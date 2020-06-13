# Veggie at my place (Python project)

Veggie at my place (VAMP) is an organisation where students are put into teams. The students within a team then cook food for each other over the next few weeks.

This notebook will tackle a problem which VAMP and many other student/organisations could potentially face. The issue is how to assign a group of people into teams. Currently the teams are assigned **manually** by the organizers where an entire day is dedicated to group students. The teams should be based on the following informal guidelines

- Gender diversity
- Diversity in nationalities
- Student who live live near each other should be paired up

The formal name of this problem is known as *matching* in graph theory.  However, the formalization could get a bit complicated for someone who is not familiar with discrete optimization. Therefore the python script only covers a manual approach using pandas commands to make the grouping easier. The last section of this document covers how one could formalize this problem where less manual work is needed. However this does require a bit of pre-planning and set up.



These criteria is very informal (non-numeric) which makes the problem hard the compute. It is also hard for the organizers to describe the above criteria formally since they don't know the how the in



## Maximum weight matching

### Matching problem introduction

The input is a bipartite graph where the nodes could be grouped into *X* and *Y*. The property of a bipartite graph is that there is no edges between the nodes in *X* and the same for the nodes in *Y*. However there are edges between *X* and *Y* with associated edge weight.

The Matching problem boils down to choosing a set of edges which maximizes the edge weight. The constraints to this problem is that every node can only be associated with one edge. In other words only one node from *X* can be matched up with a nodes from *Y* and vice versa.

### Matching problem with VAMP

The first part of the script needs to divide the data into two parts (note these *X* and *Y*). This will be the creation of the bipartite graph, where no students from *X* will only be matched from *Y*. Students in *X* will not be matched with each other, and the same goes for *Y*. Since gender diversity was one of the grouping guidelines, an suggestion would be to create this bipartite graph according to gender (males are put into *X* and females into *Y*).

The next step is to create the edge weights between *X* and *Y*. Given two students (one from *X* and one from *Y*) we need to evaluate the given attributes (i.e location, nationality etc..) into a single score which will be used as the edge weight.  Attributes with numeric values are easier to compute. For example if location is given in numbers 1-10 and numbers close to each other are signifying that two student live near each other. Let *a* be location of a student  in *X* and *b* be a location of student in *Y*  then the formula 1/(|a - b|)  would give a higher score for students who are located near each other.

VAMP organizers usually put 4 students into one team. Therefor this matching problem needs to be formulated again where the two matched up students are now considered one node in the graph. Then we can set up another matching optimization problem which takes two students and matches them up with two other students.

