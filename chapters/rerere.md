# ReReRe Reuse Recorded Resolution

It is a merge conflict resolving automation feature offered by Git, to resolve same merge conflict that occurs multiple times we can record conflict resolving steps and reuse them again.

> `$ git config --global rerere.enabled true`  
> you should enable this feature before resolving conflicts in order to record them.
>
> `$ git rerere status`  
> to show recorded resolutions
>
> `$ git config --global rerere.enabled false`  
> to turn this feature off
>
> delete .git/rr-cache directory to delete recorded resolution.
>
> `$ git rerere forget <recorded_resolution_name>`  
> to forget specific resolution


[Index][index]

[index]: ../index.md