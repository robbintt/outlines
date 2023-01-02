
### Some tips for using Slic3r



#### Issues rendering a preview

I had problems rendering a preview. As I brought the slider up from 0% rendered to 100% (top of model) rendered, the computer was running out of memory.

There is [a guide that has helpful information](http://slic3r.org/blog/tip-handling-large-models)

Things I did (did not help render preview without crashing):

1. Set resolution to 0.01mm (default is 0mm).
2. Set threads to 1
    - may not have mattered

Things I am doing (TBD):
3. Opened each file in meshlab, allowed it to delete duplicate vertices, and saved the file again.
    - In the original pass I did simplify mesh according to [this howto](http://www.shapeways.com/tutorials/polygon_reduction_with_meshlab)
    - See if the simplify mesh actually matters... removing duplicate vertices may have been enough


Information:

1. In `top`, CPU seemed to be the bottleneck. Memory was not observed to increase as the model rendering slowed (between 35% to 45%)
