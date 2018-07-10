#android基础部分
##Intent Service
有两个优点。
1，不用new线程。
2，Service运行完成后内存会自己回首掉

```
IntentService是Service的子类，是一个异步的，会自动停止的Service，很好的解决了Service里面耗时任务执行完成后，忘记关闭。内存泄漏的问题
```
