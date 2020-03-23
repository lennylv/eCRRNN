# eCRRNN

Readme.md 

This repository provides the companying data sets and scripts for the paper:

Buzhong Zhang, Jinyan Li and Qiang Lü. Prediction of 8-state protein secondary structures by a novel deep learning architecture. BMC Bioinformatics, (2018)19:293. 

which presents eCRRNN (the ensemble of 10 CRRNN predictors) for protein secondary structure prediction.

This repository includes CB513 and test2018 datasets. 

- CB513 is for replicating exactly results published in our paper, input with a ready 50-dim feature data file.
- Test2018 (Shapovalov, https://www.biorxiv.org/content/10.1101/2020.01.17.911065v1.abstract) is for demonstrating how to assemble 20+22+7+1=50-dim feature as the input for eCRRNN.

The running platform:

​    Linux, Python 2.7, Theano 0.9, Keras 2.0.5 and other utilities for preparing data. 

Download the package ecrrnn_q8.gz and unzip it. The folder structure and its explanation:

**/scripts**: All runnable files. 

- run_test_cb513.py: run eCRRNN on CB513 in Q8 prediction.
- cb513_compute.acc.py: calculate the accuracy of CB513 test.
- run_ecrrnn_test2018.py: run eCRRNN on test2018 in Q8 prediction.
- test2018_compute_acc.py: calculate the accuracy of test2018.
- gen_pssm.py: obtain PSSM features from raw PSSM profiles. The order of the 20-dim PSSM features is as ‘A R N D C Q E G H I L K M F P S T W Y V’, which is consistent with the original profile generated by psi-blast.
- prepare_for_input.py: obtain the input 3D matrix. Features of PSSM and physical properties are normalized to (0, 1) by logistic function. Features of sequence coding(one-hot vector) are mapped to dense vector.
- keras: keras2.0.5. 
- gen_test2018_lbl.py: obtain golden labels from test2018.

**/log**: output log files.

**/pred_out predicting**: predition output.

**/models**: Empty trained model files due to space limitation here.

​	/q8: ten trained model files for q8 prediction. Please download from http://qianglab.scst.suda.edu.cn/ecrrnn/crrnn_q8_models.tar.gz.

​    /q3: ten trained model files for q3 prediction. Please download from http://qianglab.scst.suda.edu.cn/ecrrnn/crrnn_q3_models.tar.gz.

**/data**: all data files

​    one-vec.dat  Sequence coding vectors where are used to map a one-hot vector to  a densed vector.

​    /cb513

- cb513_fasta_label.txt: residues and labels in CB513 dataset.
- cb513+profile_split1.npy: orginal CB513 dataset published by Zhou J, Troyanskaya OG. Deep supervised and convolutional generative stochastic network for protein secondary structure prediction. In: Proceedings of the 31st International Converenfe on Machine Learning (ICML). Bejing: PMLR: 2014. p. 745–53.. 
- cb513_profile_myfea50_pad700.npy: input features to eCRRNN and labels of CB513 dataset. 

​	/test2018: A test dataset for evaluating SecNet released by Maxim Shapovalov , Roland L. Dunbrack, Jr and Slobodan Vucetic(2020, https://github.com/sh-maxim/ss)

- /fasta: All 149 sequence files in fasta style.
- /labels-q8: test2018 labels of q8 secondary structures.
- /pssm: PSSM profiles generated by psi-blast.
- test2018_labels_residues.txt: All labels of q8 structure are combined in one file for convenience of computing accuracy. 
- test018-list.txt: sequences ids in test2018. 33 unknown residues and the corresponding labels in 6FHNA are removed. If length of the sequence is more than 700 and less than1400, the sequence will be split two sequences (first length/2 residues, last length/2 residues). Note: label 'L' of q8 of eCRRNN  is mapped to 'C' of SecNet. 
