### Serialization
序列化
- 为什么要？
- 需要考虑什么？
  - 序列化时间
  - 序列化后大小
- 产品对比
  - Java原生，ObjectOutputStream
  - Hession
  - ProtoBuf
  - Json
  - 


###### 自定义序列化-fastjson--参考com.alibaba.fastjson.serializer.StringCodec
```Java
public class ByteBufCodec implements ObjectSerializer, ObjectDeserializer {

    /**
     * 序列化
     * @param serializer 序列化器
     * @param object     like:UnpooledHeapByteBuf
     * @param fieldName  like:headBuf
     * @param fieldType  like:class io.netty.buffer.ByteBuf
     * @param features   parent object field serializer features
     */
    @Override
    public void write(JSONSerializer serializer, Object object, Object fieldName, Type fieldType,
                      int features) {
        SerializeWriter out = serializer.getWriter();
        if (object == null) {
            out.writeNull();
            return;
        }
        ByteBuf buf = ((ByteBuf) object);
        out.writeByteArray(buf.array());
    }

    /**
     * 反序列化
     * @param parser    解析器
     * @param type      like :class io.netty.buffer.ByteBuf
     * @param fieldName like :headBuf
     * @return re
     */
    @Override
    public <T> T deserialze(DefaultJSONParser parser, Type type, Object fieldName) {
        JSONLexer lexer = parser.getLexer();
        if (lexer.token() == JSONToken.NULL) {
            lexer.nextToken();
            return null;
        }
        return (T) Unpooled.wrappedBuffer(lexer.bytesValue());
    }

    @Override
    public int getFastMatchToken() {
        return 0;
    }
}


//使用
@JSONField(serializeUsing = ByteBufCodec.class,deserializeUsing = ByteBufCodec.class)
    private ByteBuf headBuf;

```
