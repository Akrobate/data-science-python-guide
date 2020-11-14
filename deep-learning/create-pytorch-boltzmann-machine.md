# Build a Boltzmann machine using PyTorch

Simple example of RBM

```python
class RBM():

    def __init__(self, nv, nh):
        self.W = torch.randn(nh, nv)
        self.a = torch.randn(1, nh)
        self.b = torch.randn(1, nv)

    def sample_h(self, x):
        wx = torch.mm(x, self.W.t())
        activation = wx + self.a.expand_as(wx)
        proba_hidden_given_visible = torch.sigmoid(activation)
        return proba_hidden_given_visible, torch.bernoulli(
            proba_hidden_given_visible)

    def sample_v(self, x):
        wy = torch.mm(x, self.W)
        activation = wy + self.b.expand_as(wy)
        proba_visible_given_hiden = torch.sigmoid(activation)
        return proba_visible_given_hiden, torch.bernoulli(
            proba_visible_given_hiden)

    def train(self, v0, vk, ph0, phk):
        self.W += torch.mm(v0.t(), ph0) - torch.mm(vk.t(), phk)
        # same as v0 - Vk
        self.b += torch.sum((v0 - vk), 0)
        # same as ph0 - phk
        self.a += torch.sum((ph0 - phk), 0)

```