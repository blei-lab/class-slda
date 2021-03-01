# Supervised latent Dirichlet allocation for classification

(C) Copyright 2009, Chong Wang, David Blei and Li Fei-Fei. Written by Chong Wang, chongw@cs.princeton.edu, part of code
is from [lda-c](https://github.com/Blei-Lab/lda-c).

This is a C++ implementation of supervised latent Dirichlet allocation (sLDA) for classification. Note that the code here is slightly different from what was described in [2] in order to speed up. Note that this is only the sLDA. The annotation part is not yet posted.

## Sample data

A preprocessed 8-class image dataset [2] from [Labelme](http://labelme.csail.mit.edu/). See [images.tgz](./sample-data/images.tgz).

UIUC Sports annotation files: [annotations](./sample-data/uiuc-sports-annotations.txt) and [meta information](./sample-data/uiuc-sports-info.txt). The source image files can be found [here](http://vision.stanford.edu/lijiali/event_dataset/). (Note: there might be some discrepancies and it is unclear why...)

## References

[1] Chong Wang, David M. Blei and Li Fei-Fei. Simultaneous image classification and annotation. In CVPR, 2009. [[PDF]](http://www.cs.columbia.edu/~blei/papers/WangBleiFeiFei2009.pdf)

[2] David M. Blei and Jon McAuliffe. Supervised topic models. In NIPS, 2007. [[PDF]](http://www.cs.columbia.edu/~blei/papers/BleiMcAuliffe2007.pdf)


---

## README

Note that this code requires the Gnu Scientific Library, http://www.gnu.org/software/gsl/

------------------------------------------------------------------------


TABLE OF CONTENTS


A. COMPILING

B. ESTIMATION

C. INFERENCE


------------------------------------------------------------------------

A. COMPILING

Type "make" in a shell. Make sure the GSL is installed.


------------------------------------------------------------------------

B. ESTIMATION

Estimate the model by executing:

     slda [est] [data] [label] [settings] [alpha] [k] [seeded/random/model_path] [directory]

The saved models are in two files:

     <iteration>.model is the model saved in the binary format, which is easy and
     fast to use for inference.

     <iteration>.model.txt is the model saved in the text format, which is
     convenient for printing topics or analysis using python.
     

The variational posterior Dirichlets are in:

     <iteration>.gamma


Data format

(1) [data] is a file where each line is of the form:

     [M] [term_1]:[count] [term_2]:[count] ...  [term_N]:[count]

where [M] is the number of unique terms in the document, and the
[count] associated with each term is how many times that term appeared
in the document. 

(2) [label] is a file where each line is the corresponding label for [data].
The labels must be 0, 1, ..., C-1, if we have C classes.


------------------------------------------------------------------------

C. INFERENCE

To perform inference on a different set of data (in the same format as
for estimation), execute:

     slda [inf] [data] [label] [settings] [model] [directory]
    
where [model] is the binary file from the estimation.
     
The predictive labels are in:

     inf-labels.dat

The variational posterior Dirichlets are in:

     inf-gamma.dat
