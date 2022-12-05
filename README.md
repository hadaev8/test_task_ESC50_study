# Audio Classification with 1d ConvNeXt: Investigating the effects of regularization techniques on model performance

[Train logs](https://wandb.ai/had/esc50?workspace=user-had)

This project is focused on comparing the performance of a baseline model and 1d [ConvNeXt](https://arxiv.org/abs/2201.03545) model on the [ESC-50 dataset](https://github.com/karolpiczak/ESC-50), which is a collection of 2000 environmental audio recordings labeled with 50 different classes.

The project aims to investigate the effects of various techniques, such as dropout, [SAM](https://github.com/davda54/sam), self-supervision, and training on raw data or learned features from [EnCodec](https://github.com/facebookresearch/encodec), on the model's ability to generalize and classify audio recordings accurately in a limited Google Colab setting.

## Model architecture

The HiFiGANClassifier model is a discriminator from the [HiFiGAN vocoder](https://arxiv.org/abs/2010.05646) model, which is a well-known model for working with raw audio waves.

The ConvNeXt architecture, on the other hand, is a recently proposed model that aims to improve on the standard ResNet architecture.
It was chosen for this task due to its performance and quality, as well as its theoretical connection with the transformer architecture, which is commonly used for one-dimensional data.

## Raw data vs learned features

Feature extraction from data does not always extract the useful data needed for the task, so I compared approaches to training on raw data and extracting learned features from the EnCodec.

## Generalization

In limited data settings, neural network models with a large capacity can easily overfit the training data, while models with a small capacity may struggle to generalize. Therefore, I applied various methods to improve the generalization of larger, overparameterized models.

SAM (Sharpness-Aware Minimization) is a technique for efficiently improving generalization by using optimizer with two learning steps for smoother gradient descent, which trades train time for test accuracy and generalization.

Self-supervision is a technique that helps to enforce a model to fit data better by using self-supervision. For this project, I trained the ConvNeXt model with causal convolution and LM task on EnCodec VQ codes.


## Conclusion

In the end, the baseline model achieved the best validation accuracy, while the ConvNeXt models showed signs of overfitting. Surprisingly, the self-supervision technique did not provide any additional benefits, and the effects of SAM were unclear. However, dropout, as expected, did help improve the model's performance.

Further experimentation with different model architectures and regularization techniques may improve the performance of the model.
