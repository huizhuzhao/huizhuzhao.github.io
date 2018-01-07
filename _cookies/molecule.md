---
layout: page
title: molecule 
image_path: http://obmpvqs90.bkt.clouddn.com/c1ccccc1o.jpg
---

Cyclohexanol (c1ccccc1O) is the organic compound with the formula (CH2)5CHOH.
The molecule is related to cyclohexane ring by replacement of one hydrogen atom by a hydroxyl group.[4]
This compound exists as a deliquescent colorless solid with a camphor-like odor, which, when very pure,
melts near room temperature. Billions of kilograms are produced annually, mainly as a precursor to nylon. 

Source [wiki](https://en.wikipedia.org/wiki/Cyclohexanol)

![](http://olcglpvgr.bkt.clouddn.com/c1ccccc1o.jpg?imageView2/2/w/200)

----
## paper list

#### 综述

* Drug discovery effectiveness from the standpoint of therapeutic mechanisms and indications，Hsin-Pei Shih1, Xiaodan Zhang2 and Alex M. Aronov1, 2017

* Opportunities and obstacles for deep learning in biology and medicine. https://greenelab.github.io/deep-review/


#### 小分子矢量化

* Convolutional Embedding of Attributed Molecular Graphs for Physical Property Prediction (Connor W. Coley, Regina Barzilay, William H. Green, Tommi S. Jaakkola, and Klavs F. Jensen, 2017)

* **Learning Graph Representations with Embedding Propagation**, Alberto García-Durán, Mathias Niepert, (NIPS 2017)


#### 分子相似性 Molecular Similarity

* Computer-Assisted Retrosynthesis Based on Molecular Similarity, Connor W. Coley, Luke Rogers, William H. Green, and Klavs F. Jensen, 2017

#### ADMET

* XenoSite: Accurately Predicting CYP-Mediated Sites of Metabolism with Neural Networks, Jed Zaretzki, Matthew Matlock, and S. Joshua Swamidass, 2013 (代谢位点，氘代）
  
#### 分子能预测 (energy, potentials)

* **Atom-centered symmetry** functions for constructing high-dimensional neural network potentials, Jörg Behler, 2011
  >PESs (potential energy surface, atomic positions --> **symmetric function**)

#### 分子生成 (generating molecules)

* Generating Focussed Molecule Libraries for Drug Discovery with Recurrent Neural Networks, Marwin HS Segler, Thierry Kogej, Christian Tyrchan and Mark P Waller, 2017
  >In de novo drug design, computational strategies are used to generate novel molecules with good affinity to the desired biological target. In this work, we show that recurrent neural networks can be trained as generative models for molecular structures, similar to statistical language models in natural language processing. We demonstrate that the properties of the generated molecules correlate very well with the properties of the molecules used to train the model. In order to enrich libraries with molecules active towards a given biological target, we propose to fine-tune the model with small sets of molecules, which are known to be active against that target. Against Staphylococcus aureus, the model reproduced 14% of 6051 hold-out test molecules that medicinal chemists designed, whereas against Plasmodium falciparum (Malaria) it reproduced 28% of 1240 test molecules. When coupled with a scoring function, our model can perform the complete de novo drug design cycle to generate large sets of novel molecules for drug discovery.

* ChemTS: An Efficient Python Library for de novo Molecular Generation, Xiufeng Yang, Jinzhe Zhang, Kazuki Yoshizoe, Kei Terayama, and Koji Tsuda, 2017 (RNN+MCTS)

* MDTS: automatic complex materials design using Monte Carlo tree search, Thaer M. Dieb, Shenghong Ju, Kazuki Yoshizoe, Zhufeng Hou, Junichiro Shiomi, and Koji Tsuda, 2017

#### 蛋白质二级结构预测

* Protein structure [link](http://www.particlesciences.com/docs/technical_briefs/TB_8.pdf)
  
    一篇介绍蛋白质结构的短篇（仅两页）

* Predicting Backbone Calpha angles and dihedrals from protein sequences by stacked sparse auto-encoder deep neural network (2014)

    早期的一篇利用神经网络模型来预测 theta 和 tau，（之前的模型都是预测 helix, sheet, coil 和 phi, psi)

* Improving prediction of secondary structure, local backbone angles, and solvent accessible surface area of proteins by iterative deep learning (2015)
  
    利用迭代的结构来预测二级结构

* Capturing non-local interactions by long short term memory bidirectional recurrent neural networks for improving prediction of protein secondary structure, backbone angles, contact numbers, and solvent accessibility (2017)
    
    利用循环神经网络来预测二级结构

* Analysis of deep learning methods for blind protein contact prediction in CASP12, Sheng Wang, Siqi Sun and Jinbo Xu, 2017
  >Following the CASP definition, we say two residues form a contact if in the native structure, the distance of their Cβ atoms is less than 8Å
  
  
#### 蛋白质矢量化

* Predicting protein-protein interactions based only on sequences information. Shen JW, et al. Proc Natl Acad Sci U S A. 2007;104(11):4337–41. (Cojoint traid method)
    
    将20种氨基酸分为7组，然后对序列采用宽度为3的滑窗计算频率

* Predicting protein-protein interactions from primary protein sequences using a novel multi-scale local feature representation scheme and the random forest. You ZH, et al. PLoS One. 2015;10(5):e0125811
    
    计算序列中不同位置之间的相关性 (Autocovariance method)


#### 蛋白质+小分子亲和力 (Binding affinity)

* Protein-Ligand Scoring with Convolutional Neural Networks (Matthew Ragoza, Joshua Hochuli, Elisa Idrobo, Jocelyn Sunseri, and David Ryan Koes, 2016)

* Protein–protein binding affinity prediction on a diverse set of structures (Iain H. Moal, Rudi Agius and Paul A. Bates, 2011)

* NNScore: A Neural-Network-Based Scoring Function for the Characterization of Protein-Ligand Complexes, Jacob D. Durrant and J. Andrew McCammon, 2010

* Performance of machine-learning scoring functions in structure-based virtual screening, Maciej Wójcikowski, Pedro J. Ballester & Pawel Siedlecki, 2016


#### 蛋白结合位点 (binding-site)
* DeepSite: Protein binding site predictor using 3D-convolutional neural networks
  
    将蛋白质的 3D 数据进行体素化，从而将其看作 3D 的 image（并有多个channels）；以此为输入预测每个体素是 binding-site 的概率。类似于图片的 segmentaion 模型

* A simple method for finding a protein’s ligand-binding pockets, Seyed Majid Saberi Fathi and Jack A Tuszynski, 2014


#### 非监督式学习
* Unsupervised representation learning with deep convolutional generative adversarial networks

* Seq2seq Fingerprint: An Unsupervised Deep Molecular Embedding for Drug Discovery, Zheng Xu etc. (2017)

    may be usefull to chem molecules/protein datasets


#### 多任务学习/迁移学习 (Multitask Learning/transfer learning)

* Consistent Multitask Learning with Nonlinear Output Relations, Carlo Ciliberto, Alessandro Rudi, Lorenzo Rosasco, Massimiliano Pontil, (NIPS 2017)

* Learning Multiple Tasks with Multilinear Relationship Networks, Mingsheng Long, Zhangjie Cao, Jianmin Wang, Philip S. Yu, (NIPS 2017)

* Label Efficient Learning of Transferable Representations across Domains and Tasks, Zelun Luo, Yuliang Zou, Judy Hoffman, Li Fei-Fei, (NIPS 2017)

* Low Data Drug Discovery with One-shot Learning, Han Altae-Tran, Bharath Ramsundar, Aneesh S. Pappu, and Vijay Pande, (2016)

* Active One-shot Learning, Mark Woodward, Chelsea Finn, (2017)

<!--
![c1ccccc1o](/images/molecule/c1ccccc1o.png?imageView2/2/h/20)
-->


<!--
Aspirin (CC(=O)OC1=CC=CC=C1C(=O)O)  also known as acetylsalicylic acid (ASA), is a medication used to treat pain, fever, and inflammation.[3] Specific inflammatory conditions in which it is used include Kawasaki disease, pericarditis, and rheumatic fever. Aspirin given shortly after a heart attack decreases the risk of death. Aspirin is also used long-term to help prevent heart attacks, strokes, and blood clots, in people at high risk.[3] Aspirin may also decrease the risk of certain types of cancer, particularly colorectal cancer.[4] For pain or fever, effects typically begin within 30 minutes.[3] Aspirin is a nonsteroidal anti-inflammatory drug (NSAID) and works similar to other NSAIDs but it is also an antiplatelet and suppresses the normal functioning of platelets. 

Source [wiki](https://en.wikipedia.org/wiki/Aspirin)

![](http://olcglpvgr.bkt.clouddn.com/aspirin_2.png?imageView2/2/w/300)


CCc1cccc2ccccc12

![](http://olcglpvgr.bkt.clouddn.com/CCc1cccc2ccccc12.png?imageView2/2/w/300)
-->
