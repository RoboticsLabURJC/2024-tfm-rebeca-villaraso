# Training
For this example we used SuperGradients to ease the training process. But the workflow would be very similar with any other custom model or framework.

Firstly, the images are parsed into the dictionaries and the Datadicts are created with their information. These are then passed into a Dataloader object in order to use them with the SuperGradients Trainer.

Then the Trainer is configured and the model is loaded. In this case, the pre-trained weights with the Cityscapes datasets are loaded.

Lastly the trainig is started.


# Super Gradients documentation and tutorial

https://docs.deci.ai/super-gradients/latest/documentation/source/welcome.html
