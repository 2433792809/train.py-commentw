 训练脚本中的初始化代码注释
——————————————————————————————————————————
-------------------------------------------------------------------------------------------------------------------------------------------------------------
✔训练前应当做的初始化
---------------------------------------------------------------------------------------------------------------------------------------------------------
启动⼀个 Pytorch 训练⼯程之前，我们要配置好所有要⽤上的东⻄，除了数据集之外，我们还有什么是要初始化的呢？

答：


✔训练脚本中的初始化代码注释
---------------------------------------------------------------------------------------------------------------------------------------------------------
    self.device = torch.device('cuda:0' if args.is_cuda else'cpu') 

这段代码是在PyTorch中用于设置设备（device）的。如果args.is_cuda为True，则将设备设置为GPU；否则将设备设置为CPU。

torch.device函数用于创建一个PyTorch设备对象，接受一个字符串参数，表示设备名称。当参数为'cuda:0'时，表示使用第一个可用的GPU设备；当参数为'cpu'时，表示使用CPU设备。
因此，这段代码的作用是将设备设置为GPU（如果可用），否则设置为CPU，以便在训练或推理期间执行相应的计算。

---------------------------------------------------------------------------------------------------------------------------------------------------------
    'num_workers': args.num_workers

这段代码是在设置PyTorch数据加载器（DataLoader）的参数。其中，num_workers参数表示用于数据加载的子进程数量。在这段代码中，args.num_workers表示使用命令行参数args中指定的子进程数量来加载数据。因此，这段代码的作用是根据args参数中的num_workers值，设置数据加载器使用的子进程数量。

num_workers参数决定了数据加载器将会启动多少个子进程来预先加载数据，以提高训练效率。默认情况下，该参数值为0，即表示不使用子进程来加载数据。如果将该参数设置为一个正整数，那么数据加载器将会启动相应数量的子进程来加载数据。通常情况下，这个值可以根据机器的CPU核心数来设置。

---------------------------------------------------------------------------------------------------------------------------------------------------------
    train_dataset = datasets.ImageFolder(
    args.train_dir, # ?
    transform=transforms.Compose([
    transforms.RandomResizedCrop(256), # ?
    transforms.ToTensor() # ?
     ])
     )
 
 args.train_dir：表示训练数据集所在的目录路径。
 
 transforms.RandomResizedCrop(256): 是 PyTorch 中的一个图像预处理操作，用于将输入的图像随机裁剪为指定大小。具体来说，该函数会按照以下步骤进行处理：

从原始图像中随机选择一个矩形区域。

将该区域按照指定的大小（256x256）进行裁剪，并将其缩放为指定的大小.

返回裁剪并缩放后的图像。

transforms.ToTensor() :是将输入的图像转换为张量形式，以便可以被输入到 PyTorch 模型中进行训练或预测。

---------------------------------------------------------------------------------------------------------------------------------------------------------
    self.train_loader = DataLoader(
    dataset=train_dataset, # ?
    batch_size=args.batch_size, # ?
    shuffle=True, # ?
    **kwargs
     )
     
 dataset=train_dataset：是将训练数据集传递给数据加载器，以便批量加载训练数据。
 
 batch_size=args.batch_size：是将每个批次中包含的样本数传递给数据加载器，以便批量加载训练数据
