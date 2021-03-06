DenseNet with TensorFlow
~~~~~~~~~~~~~~~~~~~~~~~~

Two types of `Densely Connected Convolutional Networks <https://arxiv.org/abs/1608.06993>`__ (DenseNets) are available:

- DenseNet - without bottleneck layers
- DenseNet-BC - with bottleneck layers

Each model can be tested on such datasets:

- Cifar10
- Cifar10+ (with data augmentation)
- Cifar100
- Cifar100+ (with data augmentation)
- SVHN

A number of layers, blocks, growth rate, image normalization and other training params may be changed trough shell or inside the source code.

Example run:

.. code::

    python run_dense_net.py --train --test --dataset=C10

List all available options:

.. code:: 
    
    python run_dense_net.py --help

There are also many `other implementations <https://github.com/liuzhuang13/DenseNet>`__ - they may be useful also.

Citation:

.. code::
     
     @article{Huang2016Densely,
            author = {Huang, Gao and Liu, Zhuang and Weinberger, Kilian Q.},
            title = {Densely Connected Convolutional Networks},
            journal = {arXiv preprint arXiv:1608.06993},
            year = {2016}
     }

Test run
--------
For model validation I preformed various test runs with different image normalization.
At first normalization when we divide full image by 256 works better that normalization by channels.
But after I while, normalization per channels was fixed - and it seems to perform nearly the same or better than dividing normalization.

====================== ====== ====== ===== ====== ======= ====== ======
Normalization -->>            by channels  divide by 256  paper results
----------------------------- ------------ -------------- -------------
Model type             Depth  C10    C100    C10    C100   C10    C100
====================== ====== ====== ===== ====== ======= ====== ======
DenseNet(*k* = 12)     40     6.67   27.44   6.51   27.92   7.00  27.55
DenseNet-BC(*k* = 12)  100    5.54   24.88   --     24.87   5.92  24.15
====================== ====== ====== ===== ====== ======= ====== ======

Approximate training time for models on GeForce GTX TITAN X GM200 (12 GB memory):

- DenseNet(*k* = 12, *d* = 40) - 17 hrs
- DenseNet-BC(*k* = 12, *d* = 100) - 1 day 18 hrs


Difference compared to the `original <https://github.com/liuzhuang13/DenseNet>`__ implementation
---------------------------------------------------------
The existing model should use identical hyperparameters to the original code. If you note some errors - please open an issue.

Also it may be useful to check my blog post `Notes on the implementation DenseNet in tensorflow. <https://medium.com/@illarionkhlestov/notes-on-the-implementation-densenet-in-tensorflow-beeda9dd1504#.55qu3tfqm>`__

Dependencies
------------

- Model was tested with Python 3.4.3+ and Python 3.5.2 with and without CUDA.
- Model should work as expected with TensorFlow >= 0.10. Tensorflow 1.0 support was recently included.

Repo supported with requirements file - so the easiest way to install all just run ``pip install -r requirements.txt``.

