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

Using the class

```python 
nv = len(training_set[0])
nh = 100

batch_size = 100

rbm = RBM(nv, nh)

# RBM Training
nb_epoch = 10

# Epoch loop
for epoch in range(1, nb_epoch + 1):
    train_loss = 0
    s = 0.0
    # Batch loops
    for id_user in range(0, len(training_set) - batch_size, batch_size):
        v0 = training_set[id_user:id_user + batch_size]
        vk = v0
        ph0, _ = rbm.sample_h(v0)
        for k in range(10):
            _, hk = rbm.sample_h(vk)
            _, vk = rbm.sample_v(hk)
            vk[v0 < 0] = v0[v0 < 0]
        phk, _ = rbm.sample_h(vk)
        rbm.train(v0, vk, ph0, phk)
        train_loss += torch.mean(torch.abs(v0[v0 >= 0] - v0[v0 >= 0]))
        s += 1.0
    print("epoch: " + str(epoch) + " loss: " + str(train_loss / s))

```