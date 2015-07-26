codebook.md

Script/ file name: run_analysis.R

Overall approach outlined below;  broken down into sections related to the tasks.  Comments are also included in the run_analysis.R file

1.  	Assumed file was already downloaded, and unzipped into current folder.  
1.1 	erase all local files (helped with backtesting)
1.2 	loaded libraries (plyr), (dply), and (data.table)

1.3  	Reads in y_test (dim 2947 x 1) and x_test (dim 2947 x 561) and also subject_test (dim 2947 x 1)
1.4 	Reads in y_train (dim 7352x 1) and x_train(dim 7352 x 561) and also subject_train (dim 7352 x 1)
1.5 	Reads in features.txt (dim 561 x 2)

1.6 	Column names generated from features[2]
		(checked for duplicates of column names in features)

1.7 	activity and subject columns added to x_train and x_test  (now, both widths are 563)
1.8		created a large merged file (MAIN) by rbind of x_train and x_test; (same number of cols)
		this resulted in some duplicate columns, but these werent essential for the final measure, so were discarded anyway
		
2.		mean and std columns isolated using grep ("mean|std") and ignore.case
		also added subject and activity columns (562, 563) as these would have been missed otherwise
		newMain created, limited to mean and std colums + subject + activity, (88 columns wide)
		
3.		made an activity_list string; used a for/next loop to rename newMain$activity, replacing 1,2,3...6 values to activity_list strings

4.  	descriptive labels;  mainly replaced t to Time and f to Freq;  also BodyBody to Body and tBody to TimeBody...
		I generally thought the other namings were fairly evident and different enough; lengthening each abbreviation looked too wordy; however could be easily done
4.1 	Also changed subject number (1-30) to "subject 1" etc... in the end I realised that the subject order was 1, 10, 11...19, 2, 20, 21, 22... 29, 3, 30, 4, 5, ... 9
		
5.		final tidy data set using aggregate, then order.  
5.1		Txt file made using suggested settings.  
