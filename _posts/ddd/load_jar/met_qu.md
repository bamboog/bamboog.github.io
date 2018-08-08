

## 遇见的问题
- 平台项目调用扩展项目jar包的时候,因为接口实现的地方入参使用了参数子类作为参数
  - Caused by: java.lang.RuntimeException: java.lang.NoSuchMethodException:
  -
  ``` java
  public interface BuildRefundContextExtension {
      void process(BaseRefundContext<BaseRefundParam, Result<?>> context);
  }

  ApplyRefundContext applyRefundContext = new ApplyRefundContext();

  //调用
  XX.process()
  //
  public class ApplyRefundContext extends BaseRefundContext<ApplyRefundParam, Result<ApplyRefundInfo>> {}

  ```
