---
layout: post
title: "PyTorch Continue Training"
description: "PyTorch Continue Training"
categories: [PyTorch]
tags: [PyTorch]
redirect_from:
  - /2020/10/06/
---
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

On the [PyTorch documentation][1], saving and loading models seem extremely easy.
```
torch.save(model, PATH)
model = torch.load(PATH)
model.eval()
```

I implemented this, and test out with the following procedure:
1.  Train a few epochs with a for loop. Record the validation loss and save the model once in a while using ***torch.save(model, PATH)***.
2.  Stop training once the validation loss improves clearly.
3.  Load the saved model and evaluate using ***model = torch.load(PATH)*** and ***model.eval()***
4.  Continue training

Step 3 gives me the same scale of loss as in step 2, but when I resume training in step 4, the loss restarts from the scale in step 1.

---
# Load all the states
It turns out that if we want to resume training, we also need to save the optimizer parameters. I implement the code suggested [here][2], and the modifications are:

1.  Save the optimizer states as well.
```
state = {'epoch': epoch + 1,
         'model': model.state_dict(),
         'optimizer': optimizer.state_dict()}
torch.save(state, filename+'.pt')
```
2.  Same as before.
3.  Define the model and optimizer, and load the parameters using this function
```
def load_checkpoint(model, optimizer, filename='checkpoint.pth.tar'):
    start_epoch = 0
    if os.path.isfile(filename):
        print("=> loading checkpoint '{}'".format(filename))
        checkpoint = torch.load(filename)
        start_epoch = checkpoint['epoch']
        model.load_state_dict(checkpoint['state_dict'])
        optimizer.load_state_dict(checkpoint['optimizer'])
        print("=> loaded checkpoint '{}' (epoch {})"
                  .format(filename, checkpoint['epoch']))
    else:
        print("=> no checkpoint found at '{}'".format(filename))

    return model, optimizer, start_epoch
```
4. After loading the states, we also need to assign the states to the right device.
```
model, optimizer, start_epoch = load_checkpoint(model, optimizer, filename)
    model = model.to(device)
    for state in optimizer.state.values():
        for k, v in state.items():
            if isinstance(v, torch.Tensor):
                state[k] = v.to(device)
```

[1]https://pytorch.org/tutorials/beginner/saving_loading_models.html
[2]https://github.com/pytorch/pytorch/issues/2830
