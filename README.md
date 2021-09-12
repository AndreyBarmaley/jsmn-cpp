# JSON C++ Wrapper
This is a simpe C++ interface over [JSMN parser](https://github.com/zserge/jsmn)

![structure](https://github.com/AndreyBarmaley/JsonWrapperCpp/blob/main/classes.png)

## How to use it

read file content `SWE::JsonContentFile jc(file);` or string content `SWE::JsonContentString jc(str);`

determine type array or object
```
if(jc.isObject())
{
    // JsonObject type
    auto jo = jc.toObject();
}
else
if(jc.isArray())
{
    // JsonArray type
    auto ja = jc.toArray();
}
else
    throw std::runtime_error("not json");
```

parse primitives for *JsonObect*
```
    std::cout << "variant 1 -" << std::endl;
    for(auto & key : jo.keys())
    {
        auto type = jo.getType(key);
        std::cout << key << ": ";

        switch(type)
        {
            case JsonType::Null:        std::cout << "null"; break;
            case JsonType::Integer:     std::cout << jo.getInteger(key); break;
            case JsonType::Double:      std::cout << jo.getDouble(key); break;
            case JsonType::String:      std::cout << jo.getString(key); break;
            case JsonType::Boolean:     std::cout << std::boolalpha << jo.getBoolean(key); break;
            case JsonType::Object:      std::cout << "skip object"; break;
            case JsonType::Array:       std::cout << "skip array"; break;
            default: break;
        }
        std::cout << std::endl;
    }

    std::cout << "variant 2 -" << std::endl;
    for(auto & key : jo.keys())
    {
        auto jv = jo.getValue(key)
        std::cout << key << ": ";

        switch(jv->getType())
        {
            case JsonType::Null:        std::cout << jv->toString(); break;
            case JsonType::Integer:     std::cout << jv->getInteger(); break;
            case JsonType::Double:      std::cout << jv->getDouble(); break;
            case JsonType::String:      std::cout << jv->getString(); break;
            case JsonType::Boolean:     std::cout << std::boolalpha << jv->getBoolean(); break;
            case JsonType::Object:      std::cout << "skip object"; break;
            case JsonType::Array:       std::cout << "skip array"; break;
            default: break;
        }
        std::cout << std::endl;
    }

    // if the key value is already known
    auto val1 = jo.getString("key1", "default value1");
    auto val2 = jo.getInteger("key2", 123);
    auto val3 = jo.getInteger("key3");
```

parse primitives for *JsonArray*
```
    std::cout << "base variant -" << std::endl;
    for(int it = 0; it < ja.size(); ++it)
    {
        auto jv = ja.getValue(it);
        switch(jv->getType())
        {
            case JsonType::Null:        std::cout << jv->toString(); break;
            case JsonType::Integer:     std::cout << jv->getInteger(); break;
            case JsonType::Double:      std::cout << jv->getDouble(); break;
            case JsonType::String:      std::cout << jv->getString(); break;
            case JsonType::Boolean:     std::cout << std::boolalpha << jv->getBoolean(); break;
            case JsonType::Object:      std::cout << "skip object"; break;
            case JsonType::Array:       std::cout << "skip array"; break;
            default: break;
        }
        std::cout << std::endl;
    }

    // convert JsonArray to std::vector
    std::cout << "convert to int vector" << std::endl;
    for(auto & val : ja.toStdVector<int>())
        std::cout << val ", ";
    std::cout << std::endl;

    // convert JsonArray to std::list
    std::cout << "convert to string list" << std::endl;
    for(auto & val : ja.toStdList<std::string>())
        std::cout << val ", ";
    std::cout << std::endl;
```
