---
layout: post
title: Applications of AI in the analysis of brain signals
subtitle: "How the field of AI has and will continue advancing our understanding of neural signals" 
date: 2021-02-19 07:51 -0600
background: 'https:////images.unsplash.com/photo-1443933223857-9ca346228f72?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1192&q=80'
published: false
---

This post is a general summary of [A survey on deep learning-based non-invasive brain signals: recent advances and new frontiers ](https://pubmed.ncbi.nlm.nih.gov/33171452/), written in November 2020 by Zhang et al. It's a 42-page paper with thorough detail and insight about how AI is playing a role in the emerging field of non-invasive brain-signal analysis. The intended audience for this paper may be researchers with backgrounds in biology and/or neuroscience who want to apply deep learning in their research, and researchers with backgrounds in computer science interested in brain signal research. 

### I. Introduction
__Invasive signals__ refer to signals collected through electrodes beneath the scalp, and __non-invasive__, signals collected through electrodes upon the scalp. This paper focuses on non-invasive brain signals.
Non-invasive signals are comparably low fidelity, the Signal-to-Noise Ratio (SNR) being only approximately 5% of the original brain signals collected. 
Non-invasive collection methods can be electrical, magnetic, or metabolic, which include Electroencephalogram (EEG), Functional near-infrared spectroscopy (fNIRS), Functional magnetic resonance imaging (fMRI), and Magnetoencephalography (MEG). 
The traditional workflow has been the following: ![a](https://i.ibb.co/pygxV87/Screen-Shot-2021-02-20-at-8-01-56-PM.png) 
1. Collect brain signals
2. Preprocess the collection
3. Extract features
4. Classify <br/>
5a. Analyze <br/>
5b. Send to BCI (such as a prosthesis or a smart device) to control equipment --> step 1

Before deep learning, there were traditional classifiers dependent on domain knowledge. There were three associated difficulties with this approach:
* Brain signals are easily corrupted by various biological and environmental factors.
* Low SNR is not easily addressed.
* Feature extraction depends on domain expertise, meaning researchers needed backgrounds in biology and neuroscience. The amount of domain expertise one had would easily impact research outcomes.

Incorporating deep learning into brain signal applications has addressed the difficulties above and offer two more advantages:
* Using DL saves time as there is no need for preprocessing and feature extraction (this is all done within deep learning models)
* Deep neural networks can capture both representative high-level features and latent dependencies through deep structures. 

### II. Deep learning models 
Supervised learning models take in a labeled dataset to learn and improve accuracy. Unsupervised models try to make sense of datasets on their own by extracting features and patterns. __Discriminative Models__ are supervised learning models. Examples include multi-layer perceptrons(MLP), recurrent neural networks (RNN), and convolutional neural networks (CNN). They take in a dataset to extract features and classify samples. __Representative models__ are unsupervised learning models, which include autoencoders (AE), restricted Boltzmann machine (RBM), and deep belief networks (DBN). They take in a dataset as input and can output a representation after extracting features. __Generative Models__ are slightly different from the past two in that their main job is not to classify, but to generate data as their name implies. Variational Autoencoders (VAE) and generative adversarial networks (GAN) can output new samples and reconstruct missing data. __Hybrid Models__ combine more than two of the aforementioned models, typical combinations being a representation model for feature extraction with a discriminative model for classification.

### III. State-of-the-art DL techniques for brain signals
Below are publications' subject brain signals and deep learning models. 
![img](https://i.ibb.co/j5YyrvD/Screen-Shot-2021-02-21-at-4-37-16-PM.png)

##### A) EEG
###### Spontaneous EEG: naturally-occurring signals as opposed to evoked
* Sleep EEG: signal data can be used to recognize sleep stages (refer to R&K rules or AASM recommendations) and to diagnose sleep disorders
    * Discriminative: CNN
    * Representative: DBN-RBM
    * Hybrid: CNN & MLP, CNN & LSTM
* Motor Imagery EEG: mental imagery of making a movement ![https://www.biorxiv.org/content/biorxiv/early/2017/10/10/198432/F2.large.jpg](https://i.ibb.co/KX5h5Rt/Screenshot-2021-02-21-F2-large-jpg-JPEG-Image-1280-1094-pixels.png)
    * Discriminative: CNN, 2-D CNN, LSTM, MLP
    * Representative: D-AE, DBN-AE, DBN-RBM
    * Generative: VAE
    * Hybrid: CNN & LSTM, Repre+ Discri
* Emotional EEG: evaluation of emotions by measuring valence, arousal, and dominance
    * Discriminative: RNN, CNN, MLP
    * Representative: DBN-RBM, RBM-AE, DBN-RBM+SVM+HMM, SAAE
    * Hybrid: RNN&MLP, D-AE&MLP, DBN&RBM
* Mental Disease EEG: diagnosis of mental diseases (epileptic seizures, depression, Alzheimer's, Parkinson's)
    * Discriminative: CNN, RNN
    * Representative: DBN-RBM, sparse D-AE
    * Hybrid: CNN & RNN, CNN & LSTM, MLP, C-AE
* Data Augmentation
    * Generative: GAN can augment data to increase classification accuracy 

###### Evoked Potentials 
* (EP)/(ERP): event-related voltage changes due to outside stimuli in ongoing EEG activity that are time-locked to sensory, motor, and cognitive events
    * VEP (visual evoked potential)
        * DBN-RBM, 2D CNN, LSTM, DBN-RBM, SVM classifier, AE model, CNN
    * AEP (auditory evoked potential)
        * CNN
    * RSVP (rapid serial visual presentation)
        * CNN, MLP, DBN, DBN-AED-AE
* SSEP: 
    * SSVEP (steady state visual evoked potential): brain oscillation evoked by flickering visual stimuli
        * CNN, RNN DBN-RBM, DBN-AE, MLP

##### B) fNIRS
* Discriminative: CNN, MLP
* Representative: AE, DBN-RBM, DBN-AE
* Generative: convolutional GAN, DCGAN, WGAN 

##### C) EG
* 1-D CNN, CNN&MLP

### IV. Guidelines on choosing appropriate DL models
Classification of sleep EEG mainly utilizes discriminative and hybrid models including CNNs and RNNs. MI EEG is most significantly researched using CNN and CNN-based hybrid models. Latent features of MI EEG signals are captured using representative models such as DBN-RBM. Emotional EEG mostly use DBN-RBM for unsupervised feature learning. Mental disease diagnosis is largely a binary classification problem, which makes it easier for models to achieve accuracy greater than 90%. CNN and D-AE are prevalent likely because both deep learning models are well known for their effective classification and dimensionality reduction. In comparison, there are fewer deep learning studies on fNIRS images even though fNIRS also is known for its high portability and low cost.
###### Discriminative
The reason CNN is so prevalent is likely because of its outstanding performance in feature learning. CNN is powerful enough to extract latent discriminative features and spatial dependencies from EEG signals for classification. It is also an extremely popular model in popular research areas such as computer vision, which studies how computers can gain insight from images or videos. Because some brain signal diagrams (e.g. fMRI) are 2D images, they can be used as input to CNNs without much work. CNNs also have plenty of variations that can be adapted to different scenarios.  

But aren't brain signals technically sequential, temporal information? What about RNNs, which are great for processing that kind of information? RNNs take a long time processing long sequences (basically brain signals), and although depending on the situation, RNNs may take up more than 20 times the training time than CNN may. However, RNNs are promising in detecting epileptic seizures due to their excellent temporal dependency searching ability. By definition, spatial data is better analyzed by CNNs and temporal data, by RNNs.

###### Representative 
DBNs, particularly DBN-RBMs, are most popular for feature extraction likely because DBNs learn the generative parameters that reveal the relationship between variables in neighboring layers efficiently. DBNs also make the calculation of the latent variables(hidden variables in hidden layers) straightforward. However, most of the work using the DBN-RBM model was done before 2016. At the moment, most studies use CNN and hybrid models for both feature learning and classification. 

###### Generative
These are rare and are prevalent in data augmentation and reconstruction in fMRI and EEG signals.

###### Hybrid
RNN and CNN combos are incredibly popular for their excellent temporal and spatial feature extraction. CNN and MLP combos can also extract spatial features and classify. The generic combo of representative and discriminative models (e.g. CNN+ AE, CNN+ DBN-RBM)is also popular as the former refine features and the latter classifies. 


### V. Open Issues
Although deep learning has solved a lot of the performance issues of brain signal systems, there are still challenges including implementing an explainable general framework, subject-independent classification, semi-supervised and unsupervised classification, online implementation, and portability. 
__General frameworks__ need to be able to handle brain signals regardless of the number of channels used for signal collection, the sample dimensions, and stimulation types. They need two key capabilities: an attention mechanism, which would guarantee that the framework can focus on the most valuable parts of input signals, and the ability to capture latent features. 