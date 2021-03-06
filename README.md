# iNCML-DNNLM
A CUDA-C implementation of FOFE and FSMN

================================================================================

For technical details on:

i) FOFE: refer to

[1] S. Zhang, H. Jiang, M. Xu, J. Hou, L. Dai, ”The Fixed-Size Ordinally-Forgetting Encoding Method for Neural Network Language Models,” Proc. of Annual Meeting of the Association for Computational Linguistics (ACL 2015), July 2015.  (http://anthology.aclweb.org/P/P15/P15-2081.pdf)

ii) FSMN: refer to

[2] S. Zhang, H. Jiang, S. Wei, L. Dai, “Feedforward Sequential Memory Neural Networks without Recurrent Feedback,” arXiv:1510.02693. (http://arxiv.org/abs/1510.02693)

[3] S. Zhang, C. Liu, H. Jiang, S. Wei, L. Dai and Y. Hu, “Feedforward Sequential Memory Networks: A New Structure to Learn Long-term Dependency,” arXiv:1512.08301. (http://arxiv.org/abs/1512.08301)


================================================================================

All files must following the naming convention of basename.{extension}. 
Examples are shown with PTB (Penn TreeBank) which is shipped with the code.
That is, the basename in the provided example is ptb.

The following sub-directory of the current directory is assumed:


1. config -- containing user-defined configuration file 
	
	An example of ptb's configration is in config. Each line describes a
	layer of the neural network. The first token is surrounded with angel 
	brackets. The rest are (option, parameter) pairs. See 
	./source/network.cpp for details of what options are supported.

2. log -- containing execution logging

	It's strongly recommended to put the logging here and name them according
	to the configuration name, e.g. ptb.config.log

3. numeric-data

  	The numeric data set returned by "numericize". It will be the input
  	to "trainer". The naming must follow
        basename.{train, valid, test}.numeric. For PTB, there should be 
        ptb.train.numeric, ptb.valid.numeric and ptb.test.numeric

4. raw-data

   	Each file is a text file, one sentence per line. The naming must follow
        basename.{train, valid, test}.txt. For PTB, there should be 
        ptb.train.txt, ptb.valid.txt and ptb.test.txt

5. source

	batch-constructor.cpp  
	batch-constructor.h    
	layer.h 
	layer.cpp   
	matrix.h   
	matrix.cu      
	network.h     
	network.cpp    
	stacktrace.h  
	numericize.cpp  
	trainer.cpp           
	vocabulary.cpp     
	evaluator.cpp  

6. model-archive

	During training, for example, ptb.config.epoch{i}, the model at the 
	beginning of the ith epoch is dumped on the disk. It's named with the 
	configuration file, followed by ".epoch{i}".



================================================================================

Using PTB as example:

1. compose your own network configuration and save it in ./config/ptb.config

2. run “prepare.sh ptb 1 10001”

3. run "trainer ptb.config ptb 0.4096 256 2 | tee log/ptb.config.log”

    learning-rate  0.4096    
    mini-batch     256    
    context window 2    


