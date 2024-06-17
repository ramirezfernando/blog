---
slug: protobufs-vs-json
title: Protobufs vs JSON
description: Protocol Buffers compared to JSON format.
authors: [fearzyn]
enableComments: true
---

What are the differences between protocol buffers (Protobufs) and JSON, and when should you use them?

<!-- truncate -->

## Useful Terminology

Before getting into what JSON and Protobufs are, here are some definitions that will be helpful to know:
- **Serialization**: the process of converting a data structure into a format that can be stored or transmitted (usually through HTTP) and reconstructed later.
- **Deserialization**: the reverse process of serialization.
- **Payload**: the part of transmitted data that is the actual intended message.

## What is JSON?

For those who aren't familiar, [JSON (JavaScript Object Notation)](https://www.json.org/json-en.html) is data interchange format typically used for transferring data between a web server and a web application. JSON data is made up of key-value pairs and supports data types like objects, arrays, strings, and numbers. 

Here is an example of JSON data:
```JavaScript
{
    "firstName": "Fernando",
    "lastName": "Ramirez",
    "age": 21,
}
```

## What are Protocol Buffers?

Protocol buffers (Protobufs) are Google's a data interchange format. You define how you want your data to be structured once, then you can use special generated source code to easily write and read your structured data to and from a variety of data streams and using a variety of languages. 

To get started using Protobufs, we'll need to create a `.proto` file, like so:
```
message Person {
    string firstName = 1;
    string lastName = 2;
    uint8 age = 3;
}
```

This file defines the payload schema: data fields and types. The " = 1", " = 2", " = 3" markers on each element identify the unique “tag” that field uses in the binary encoding. 

We can then compile the `.proto` file using the Protobuf compiler to language-specific source files which can then be used to manipulate the corresponding protocol buffer. 



## Comparison

### Efficiency
A comparison between Protobufs and JSON was made by Auth0 in their article [Beating JSON performance with Protobuf](https://auth0.com/blog/beating-json-performance-with-protobuf/). In summary, If services running JavaScript and Java communicate with each other - there's not much performance improvement with Protobuf. But if services aren't running JavaScript, Protobuf performance was up to 6x better compared to JSON.

### Pros and Cons

Here are top 3 pros and cons for both JSON and Protobuf format:

#### JSON 

Pros
- Easy to use and human-readable
- Easy to change. Because it provides a flexible schema
- Support for many programming languages

Cons
- No support for schema validation
- Poor performance for big payloads
- Backward compatibility problems

#### Protobuf 

Pros
- Support for schema validation
- Improved performance with big payloads. Because it uses the binary format
- Support for backward compatibility

Cons
- Hard to debug. And not human-readable
- Extra effort to update the proto file needed
- Limited language support compared to JSON

:::note

Protobufs do support JSON, which allows you to convert between the binary Protobuf format and JSON representation - which can be used for better readability when needed.

:::

## Takeaways

Use Protobufs when:
- The payload is big
- Communication between non-JavaScript environments needed
- Frequent changes to the payload schema expected

Use JSON when:
- Simplicity needed
- High performance is not needed
- Communication between JavaScript and Node.js or other environments needed

To learn more about Protobufs, check out their docs, [here](https://protobuf.dev/)!

<br />