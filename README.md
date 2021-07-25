# hrut, the How-aRe-yoU-Today script

This script accommodates your wellbeing. It will tell you how much you should work today, in terms of your normal workload. (So the outcome is a percentage.) It does so by asking you how you feel, on a scale from 1 to 5. It will then recommend the percentage mentioned above, and adds it into a(n exponential) moving average that's saved.

The main idea is that when you feel bad/overwhelmed, you can give a low answer 1 or 2 to the script, it will reduce your workload for that day. That is assuming that you haven't escaped work this way too often in recent days. If you do that too often, that brings the moving average down, and the script starts to increase your workload back even with low answers like 1 or 2. On the other hand, giving a high answer like 4 or 5 will recommend a higher daily workload -- saving the potential to ease it on worse days. This is again done via the moving average which is being pushed higher up on these good days.

To be more precise, the moving average is based on a time constant of 66 days, and is kept between the extremes of 100 and 114 percent. At the low end 100%, even an answer 1 results in 100% recommended workload, and answer 5 in 150%. When the average is pushed up to 106% or higher, an answer 1 will already exempt you from work for the day, and when it's up at the high end 114%, then even answer 5 is only recommending 114%. These numbers are currently hard-wired in the script and are the result of a bit of experimenting.

### Usage:

Initialise with

```
hrut -u [task name]
```

which will create some files in your `home/.hrut/` and set your initial moving average to a comfortable 110%. Subsequent applications of the same command will ask you about your mood, make the recommendation and update the moving average.

To query the latest recommendation, read the files directly in `home/.hrut/` or use

```
hrut [task name]
```

or just

```
hrut
```

this latter will give back the latest one in case you ran `hrut -u` on multiple tasks. You can feed this directly into other scripts to influence their recommendations. I'm using it in my other repos `a4t`, `orgbusy` and `cli_view_edit/wothin`.

```
hrut -p [task name]
```

or just

```
hrut -p
```

for the latest task will generate a random 0 or 1 number with probability equals the recommended workload (capped at 100% of course). This is handy if you have many small tasks you'd normally do but want to ease those on bad days. I'm using this for various daily tasks and also in my url opener `cli_view_edit/lowo`.

I'm no programmer, so please don't blame me on the quality of the code. :-) Licensed under GNU GPLv3.
