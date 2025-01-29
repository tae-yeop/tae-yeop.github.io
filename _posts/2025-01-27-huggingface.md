허깅 페이스 데이터셋 처리하는 법

## 데이터 전처리하고 허브에 푸쉬하기

멀티프로세싱으로 처리
```python
import torch
import os
import json
import datasets
from datasets import Dataset, load_dataset
from facenet_pytorch import MTCNN
from torchvision import transforms
from torch.utils.data import DataLoader
from torchvision.io import read_image
from transformers import AutoTokenizer


import concurrent.futures
num_processors = 16

mtcnn = MTCNN(image_size=512, margin=10, device='cuda', post_process=False)
to_pil = transforms.ToPILImage()

root_path = '/purestorage/project/tyk/project24/face_dataset/ffhq_wild_files'
all_items = os.listdir(root_path)
subdirectories = [os.path.join(root_path, item) for item in all_items if os.path.isdir(os.path.join(root_path, item))]



def load_json(json_path):
    try:
        with open(json_path, 'r', encoding='utf-8') as f:
            json_data = json.load(f)
            caption = json_data.get('caption', '')
            image_path = os.path.join(os.path.dirname(json_path), os.path.basename(json_path).replace('.json', '.jpg'))
            return {'image_path': image_path, 'caption': caption}
    except json.JSONDecodeError:
        print(f"Error decoding JSON file: {json_path}")
    except UnicodeDecodeError:
        print(f"Error reading file due to Unicode decode error: {json_path}")
    return None



def face_crop(examples):
    image = examples['image']
    img_cropped = mtcnn(image)
    if img_cropped is not None:
        examples['face_image'] = to_pil(img_cropped.to(torch.uint8))
    else:
        width, height = image.size

        # Calculate the coordinates for a center crop
        crop_size = 300
        left = (width - crop_size) / 2
        top = (height - crop_size) / 2
        right = left + crop_size  # Corrected
        bottom = top + crop_size  # Corrected

        # Crop and resize the image
        image_cropped = image.crop((left, top, right, bottom))
        image_resized = image_cropped.resize((512, 512))

        examples['face_image'] = image_resized

    print('examples', examples)
    examples['face_image'].save('/purestorage/project/tyk/project24/face_dataset/test.png')
    return examples


data = []
with concurrent.futures.ThreadPoolExecutor(max_workers=num_processors) as executor:
    future_to_json = {executor.submit(load_json, os.path.join(root_path, folder, file_name)): file_name
                      for folder in subdirectories
                      for file_name in os.listdir(os.path.join(root_path, folder))
                      if file_name.endswith('.json')}
    for future in concurrent.futures.as_completed(future_to_json):
        result = future.result()
        if result:
            data.append(result)


# Create a Hugging Face Dataset
dataset = Dataset.from_dict({'image': [item['image_path'] for item in data], 'caption': [item['caption'] for item in data]}).cast_column('image', datasets.Image())


dataset = dataset.map(face_crop)

print(dataset[0])
dataset.push_to_hub("ty-kim/myface", token='...')

```