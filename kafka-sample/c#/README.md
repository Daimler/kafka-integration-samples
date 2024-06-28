KafkaOauthDemo
===================

The Kafka OAuth demo shows how a customer can authenticate their client via OAuth2 to Kafka and how they can read data 
from a Kafka topic using the Kafka consumer API.

This is only a sample without support and liability to its correctness!

Prerequisite
------------

The code is based on .Net 8.0 and the Confluent.Kafka client (2.1.1).

Package Links:

* https://www.nuget.org/packages/Confluent.Kafka/
* https://www.nuget.org/packages/Newtonsoft.Json/

Refer to [c#.proj](c%23.csproj) for version details and if you want to update versions.

Our Kafka server uses Let’s Encrypt CA for SSL/TLS certificates. Confluent.Kafka library use the operating system's 
default trusted root CA certificates for secure connections. Please ensure that your system has the Let's Encrypt root 
certificates installed. These certificates are usually included in the system's trusted root store by default. If not, 
please install them manually.

For Debian/Ubuntu distributions, the system CA certificates can be updated as:
```bash
sudo update-ca-certificates
```

How to use
----------

In order to use the sample, please substitute the following parameters with those you have received via secure email.

```cs
  var clientName = "YOUR_CLIENT_NAME";                  // use the client name you have received 
  var clientId = "YOUR_CLIENT_ID";                      // use the client id you have received
  var clientSecret = "YOUR_CLIENT_SECRET";              // use the secret you have received
  var scope = "SCOPE";                                  // use the correct scope for your region
  var topic = $"vehiclesignals.{clientName}";           // use topic for the client you have received
  var consumerGroup = $"{clientName}.GROUP_ID_POSTFIX"; // you can change the postfix of your consumer group

  var bootstrapUrl = "BOOTSTRAP_URL";                   // use the correct broker url for your region
  var oauthTokenApiUrl = "OAUTH_TOKEN_API_URL";         // use the correct token API url for your region
```

after preparation, you can start the demo with

```bash
dotnet run
```

or first build with

```bash
dotnet build
```

and run the executable afterward.

Notes
-----

Confluent.Kafka client supports refreshing your oauth token automatically starting from version 2.2.0. Please update the
client library as soon as it is available to your platform. In client versions before 2.2.0, broker connections will be
closed, as soon as the token expires. The client will automatically reconnect, but you will receive error logs.

Copyright 2024 Mercedes-Benz Connectivity Services GmbH
