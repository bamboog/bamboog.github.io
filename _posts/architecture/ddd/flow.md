### ddd_flow

<flow identifyCode="TRAIN_TAKEOUT_SUBMIT_ORDER">
  <bizNodes>
  <bizNode id="test1" nodeType="Composite" coreSize="2" maxSize="2" queue="5" target="test2" sync="1" name="提交订单">
    <subNode nodeType="Single" abilityClass="com.dfire.optimus.flow.test.ability.SubmitOrderAbility" name="提交订单1">
      <extension extPoint="com.dfire.optimus.flow.test.extension.IOrderConvert" extPointImpl="com.dfire.optimus.flow.test.extension.TakeoutOrderConvert" name="外卖结果转换扩展点"/>
    </subNode>
    <subNode nodeType="Single" abilityClass="com.dfire.optimus.flow.test.ability.TrainLockTestAbility" name="加锁"/>
  </bizNode>

  <bizNode id="test2" nodeType="Single" abilityClass="com.dfire.optimus.flow.test.ability.SubmitOrderAbility" target="test3" name="提交订单2"/>

  <bizNode id="test3" nodeType="Branch" name="判断订单是否提交成功">
    <expression condition="submit == false" target="test4" name="失败"/>
    <expression condition="submit == true" target="test5" name="成功"/>
  </bizNode>

  <bizNode id="test4" nodeType="Single" abilityClass="com.dfire.optimus.flow.test.ability.SubmitOrderAbility" name="提交订单3"/>

  <bizNode id="test5" nodeType="Single" abilityClass="com.dfire.optimus.flow.test.ability.SubmitOrderAbility" name="提交订单4"/>

  </bizNodes>
</flow>

- bizNode业务节点:
  - 1、id唯一节点标识（顶级bizNode需要）
  - 2、target下一节点（即对应节点的id）
  - 3、name节点信息描述
  - 4、abilityClass执行的业务逻辑
  - 5、noteType节点类型，Single同步执行，Composite并发执行，Branch分支判断：

- Composite节点下只能存放Single节点
- Single可以指定能力留下的扩展点extension（格式如上），进行调用
- Branch分支判断节点，包含expression节点（格式如上）
