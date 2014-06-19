CodeBook for run_analysis
========================================================  

0. Training and test data are opened and loaded into seperate variables: **xtest**, **ytest**, **xtrain**, **ytrain**, **subtest**, **subtrain** variables  
0.5 features and labels are opened and loaded into **labels** and **features** variables  
1. Training and test data are merged together, forming **x**,**y** and **sub** variables  
2. **x** columns are named according to features.txt file  
3. Activities contained in **y** are changed from numeric code to character, using **labels** variable  
4. The columns of **x** containing the characters "mean" or "std" are extracted into **xmean** and *xstd** and bound together into variable **xfinal**  
5. The **sub** and **y** describing the activity are added as the two last columns of **xfinal** variable.  
6. Tidy data set is created by melting **xmean** (to which **sub** and **y** have been bound), with "subject" and "activity" as the id's, and all other variables as measure.  

Methodology for all of the above can be seen in the README.md file.  