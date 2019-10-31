# seqfish-hack
seqFISH+ data in tidy format for a mini-hackathon


seqFISH+ data originally from:

* https://zenodo.org/record/2669683

This data was provided at the Oz Single Cell hackathon, however I wasn't able to make sense of it:

* https://github.com/CaiGroup/seqFISH-PLUS

From the Zenodo record, I downloaded `seqFISH+_NIH3T3_point_locations.zip`, which contained Matlab files. I then extracted mRNA locations from these files and converted them to a tidier CSV format.

run1.csv and run2.csv contain mRNA locations, from two runs of the seqFISH+ protocol, with the following columns:

* `fov` Field of view of the microscope. There are 7 FOVs in run1 and 10 in run2.
* `cell` Cell within FOV, manually curated for your convenience!
* `gene_no` Gene number, 1 to 10,000.
* `gene` Corresponding gene symbol.
* `x` x coordinate within FOV.
* `y` y coordinate within FOV.

genes.csv contains the 10,000 genes this seqFISH+ was able to detect:

* `gene_no` Gene number, 1 to 10,000.
* `gene` Corresponding gene symbol.

To get you started, here is how to plot the mRNAs from the first cell within the first FOV.

```
library(tidyverse)

run1 <- read_csv("run1.csv")

run1 %>% 
  filter(fov==1,cell==1) %>% 
  ggplot(aes(x=x,y=y)) + geom_point(alpha=0.1)

```