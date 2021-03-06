# 통계 및 수학

Created: March 15, 2022 5:29 PM

Q1) 고유값(eigen value)와 고유벡터(eigen vector)에 대해 설명해주세요. 그리고 왜 중요할까요?
    
    [Answer]
    고유벡터는 어떤 벡터에 선형변환을 취했을 때, 방향은 변하지 않고 크기만 변화되는 벡터이고 이 고유벡터를 선형변환한 결과가 원래 벡터의 몇 배가 되는지를 나타내는 값이 교유값입니다.
    고유값과 고유벡터는 행렬의 중요한 정보를 담고있는데 이러한 고유값과 고유벡터를 알면 무수히 많은 벡터의 뭉치로 되어있는 물체나 영상에서 이들이 어떤식으로 변화되고 중심축은 무엇인지에 대한 중요한 정보를 파악할 수 있습니다.
    
    - 부가 설명
      고유벡터 : 어떤 벡터에 선형변환을 취했을때, 방향은 변하지 않고 크기만 변환되는 벡터
      고유값 : 고유벡터가 변환되는 ‘크기’ (위 고유벡터를 선형변환한 결과가 원래 벡터의 몇배가 되는지를 나타내는 값)
      고유값과 고유벡터는 어떤 행렬의 가장 굉장히 중요한 정보를 담고 있다. 임의의 벡터를 어느 방향으로 변화시켰는지, 변환 과정에서 변화 없이 유지는 되는 부분은 어느 부분인지를 말한다.
         어떠한 물체나 영상 등 이들은 무수히 많은 벡터들의 뭉치라고 이야기 할 수 있는데, 고유값과 고유벡터로 인해 영상이나 물체가 어떤식으로 변화되고 중심축은 어디인지에 관한 중요한 정보들을 파악
        할 수 있다. 그렇기 때문에 응용분야에 PCA, EigenFace 가 있는 이유임을 알수 있다.
        
        [https://velog.io/@ohs2251/Eigen-vector-Eigen-value](https://velog.io/@ohs2251/Eigen-vector-Eigen-value)
        
Q2) 샘플링(Sampling)과 리샘플링(Resampling)에 대해 설명해주세요. 리샘플링은 무슨 장점이 있을까요?
    
    [Answer]
    가지고 있는 데이터 전체에 대한 조사는 사실상 불가능하기에 일부 sample을 뽑아내는 것이 샘플링이고 가지고 있는 sample에서 다시 sample 부분집합을 뽑아 변동성을 확인하는 것이 리샘플링입니다. 샘플링을 하면 전체 데이터를 나타내는 것이 아니기에 noise가 발생할 수 있는데 리샘플링을 사용하면 통계량을 늘릴 수 있기 때문에 noise를 어느정도 제거할 수 있습니다.
    
    - 부가설명
        
        Sampling: 모집단에서 임의의 sample을 뽑아내는 것으로 표본추출이라고 한다. 모집단전체에 대한 조사는 사실상 불가능 하기에 일부 sample을 뽑아서 추론한다.
        
        Resampling: 가지고있는 sample에서 다시 sample을 뽑아내어 변동성을 확인하는 것으로 같은 샘플을 여러 번 사용해서 성능을 측정하는 방식이다.
        
        → Resampling 방식에는 K-Fold Cross Validation, Bootstrap 등이 있다.
        
        [https://kejdev.github.io/posts/sampling-resampling/](https://kejdev.github.io/posts/sampling-resampling/)
        
    
Q3) 확률 모형과 확률 변수는 무엇일까요?
    
    [Answer]
    확률 변수는 확률로 표현하기 위한 사건을 정의하는 것이고 이러한 확률변수를 이용하여 데이터 분포를 근사하는 모형이 확률모형입니다.
    
    - 부가설명
        
        확률 변수 : 확률로 표현하기 위한 event를 정의하는 것
        
        - 확률변수 X = 짝수인 눈으로 정의한다.
        - 확률변수 X = 2이하의 자연수로 정의한다.
        
        확률 모형 : 수집된 데이터의 발생 확률이나 분포를 잘 근사하는 모형
        
    

---
