# Extract_DNN
A uniform framework for extracting features of DNNs

1. Install visualizer.(It is a useful tool commented in Chinese, so I describe how to use it below.)
    ```
    python setup.py
    ```
    

2. add get_local at the class of layer that you want to extract.
    ```python
    from visualizer import get_local
    @get_local('attention_map')
    def your_attention_function(*args, **kwargs):
        ...
        attention_map = ... 
        ...
        return ...
    ```
    or
    ```python
    from visualizer import get_local

    class Attention(nn.Module):
        def __init__(self):
            ...
        
        @get_local('attn_map')
        def forward(self, x):
            ...
            attn_map = ...
            ...
            return ...
    ```
3. load model and data, and predict
```python
from visualizer import get_local
get_local.activate() 
from ... import model 

# load model and data
...
out = model(data)

cache = get_local.cache # ->  {'your_attention_function': [attention_map]}
```
4. save cache after some renaming