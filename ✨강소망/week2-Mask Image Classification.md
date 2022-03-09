# Mask Image Classification - Architecture

# Data Augmentation

```python
class CustomAugmentation:
    def __init__(self, resize, mean, std, **args):
        self.transform = transforms.Compose([
            CenterCrop((320, 256)),
            Resize(resize, Image.BILINEAR),
            ColorJitter(0.1, 0.1, 0.1, 0.1),
            ToTensor(),
            Normalize(mean=mean, std=std),
            AddGaussianNoise()
        ])

    def __call__(self, image):
        return self.transform(image)
```

- CenterCrop : 가운데를 Crop
- Resize : 사이즈 조정
- ColorJitter : 명도,채도,밝기 등을 조정
- ToTensor : 텐서로 변환
- Normalize :
- GaussianNoise

# Training

- Learning Rate : 0.001~0.002
- batch size = 64
- Loss : Cross Entropy
- Epoch : 10~15
- Optimizer : Adam
- Cross-Validation : (train:val = 8:2)

# Model

[PreTrained ResNet18]

```python
class PreResNet(nn.Module):
    def __init__(self, num_classes):
        super().__init__()
        self.model = models.resnet18(pretrained=True)
        self.num_ftrs=self.model.fc.in_features
        self.model.fc=torch.nn.Linear(self.num_ftrs,num_classes)
        
        torch.nn.init.xavier_uniform_(self.model.fc.weight)
        stdv=1./math.sqrt(self.model.fc.weight.size(1))
        self.model.fc.bias.data.uniform_(-stdv,stdv)
        

    def forward(self, x):
        pass
        x=self.model(x)
        return x
```

→ EfficientNet, ResNet 깊은 레이어보다 성능이 우수함