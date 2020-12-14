# CS677_Midterm_BiT
Tasks / Rubric (100 points)
1) Write a 2 page (excluding pictures) summary of what transfer learning (10 points)

- Refer to [CS677_PAULAG_Transfer.pdf](https://github.com/paul-data-science/CS677_Midterm_BiT/blob/main/CS677_PAULAG_Transfer.pdf)

2) Write a 2 page (excluding pictures) summary of what architectural improvements, if any, the authors have assumed on top the ResNet-xyz V1 architecture and why (20 points)

- Refer to [CS677_PAULAG_ResNet_V2.pdf](https://github.com/paul-data-science/CS677_Midterm_BiT/blob/main/CS677_PAULAG_ResNet_V2.pdf)

3) Write a 4 page (excluding figures) summary of the key points that need to be made so a non-expert can understand the differences between GN, WS and BN. The top 3 comparisons will make it to my class notes with attribution. (30 points)

- Refer to [CS677_PAULAG_GN_WS_BN.pdf](https://github.com/paul-data-science/CS677_Midterm_BiT/blob/main/CS677_PAULAG_GN_WS_BN.pdf)

4) Write a 2 page (excluding figures) summary of MixUp regularization and how this may help (30 points).

- Refer to [CS677_PAULAG_Mixup_v3.pdf](https://github.com/paul-data-science/CS677_Midterm_BiT/blob/main/CS677_PAULAG_Mixup_v3.pdf)

5) Explain all models that are used in producing performance results (eg RetinaNet) (10 points)

- Refer to [CS677_PAULAG_RetinaNet.pdf](https://github.com/paul-data-science/CS677_Midterm_BiT/blob/main/CS677_PAULAG_RetinaNet.pdf)

Extra Points (20 points)
Apply the Big Transfer technique from this repo in CIFAR10 downstream dataset for 1-10 examples per class (low-data regime). 
Match the behavior of Fig 6 for one upstream dataset of your choice and ResNet50-x3 architecture (20 points).

Also refer to [Colabs folder](https://github.com/paul-data-science/CS677_Midterm_BiT/tree/main/colab)

Modifications and then Observations:
On Original pytorch_BiT nb from the BiT repo (https://github.com/google-research/big_transfer/blob/master/colabs/big_transfer_pytorch.ipynb):
1) Some lines were commented out because they were not needed for this experiment
2) Following changes were made to use 'BiT-M-R50x3' pre-trained on ImageNet: 
-	weights = get_weights('BiT-M-R50x3')
-	model = ResNetV2(ResNetV2.BLOCK_UNITS['r50'], width_factor=3, head_size=10, zero_head=True)
-	sampler = torch.utils.data.RandomSampler(train_5shot, replacement=True, num_samples=256)
-	loader_train = torch.utils.data.DataLoader(train_5shot, batch_size=32, num_workers=2, sampler=sampler)
3) **Runtimes:**
In respective order of 5 runs:
- **[Step 499] loss=1.83e-06 train accu=100.00% test accu=84.44% (lr=3e-06)**
- **[Step 499] loss=2.50e-06 train accu=100.00% test accu=84.53% (lr=3e-06)**
- **[Step 499] loss=9.46e-07 train accu=100.00% test accu=83.31% (lr=3e-06)**
- **[Step 499] loss=2.80e-06 train accu=100.00% test accu=87.93% (lr=3e-06)**
- **[Step 499] loss=1.44e-06 train accu=100.00% test accu=85.89% (lr=3e-06)**

Showing 6th run because it gave higher test acc than original BiT research paper:
- [Step 499] loss=5.12e-07 train accu=100.00% test accu=89.28% (lr=3e-06)

**Conclusion:**
- It seems the test accuracies shown above seem to behave similar to Fig 6 with ImageNet upstream dataset
and CIFAR10 downstream dataset of 5 examples (CIFAR-10) chart compared to our 1-10 examples per class (low-data regime).
