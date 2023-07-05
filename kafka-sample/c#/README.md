KafkaOauthDemo
===================

The Kafka OAuth demo shows how a customer can authenticate their client via OAuth2 to Kafka and how they can read data from a Kafka topic API and.

This is only a sample without support and liability to its correctness!

Prerequisite
------------

The code is based on .Net 7.0 and the Confluent.Kafka client (2.1.1).

Package Links:

* https://www.nuget.org/packages/Confluent.Kafka/
* https://www.nuget.org/packages/Newtonsoft.Json/

Refer to [c#.proj](c%23.csproj) for version details and if you want to update versions.

On linux systems, the client expects the hosts' ca-certificate at `/etc/pki/tls/ca-bundle.crt` (fedora/redhat defaults).
If your systems default location differs from that (e.g. Debian/Ubuntu), please make sure to copy or symlink the
certificate.

Example for Debian/Ubuntu distributions:
```bash
mkdir -p /etc/pki/tls/certs
ln -s /etc/ssl/certs/ca-certificates.crt /etc/pki/tls/certs/ca-bundle.crt
```

How to use
----------

In order to use the sample please change the following parameters. Those parameters should previously send to you.

```cs
  var clientId = "YOUR_CLIENT_ID";               // CHANGE HERE
  var clientSecret = "YOUR_CLIENT_SECRET";       // CHANGE HERE
  var topic = "TOPIC_NAME";                      // CHANGE HERE
  var consumerGroup = "CONSUMER_GROUP";          // CHANGE HERE            

  var brokerUrl = "BROKER_URL";                  // CHANGE HERE
  var oauthTokenApiUrl = "OAUTH_TOKEN_API_URL";  // CHANGE HERE
```

You also need to provide the CA certificate location.

```cs
  var rootCaFile = @"cert.pem";                  // CHANGE HERE, put here the location of your CA certificate (must be PEM file)
```

The certificate file must be in PEM format. You can extract the PEM from a .p12 using `openssl` and `sed`:

```bash
openssl pkcs12 -in cluster-ca.p12 -nokeys | \
sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > cluster-ca.crt
```

Or export it, using a GUI-based tool like [keystore explorer](https://keystore-explorer.org/)

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

Copyright 2023 Mercedes-Benz Connectivity Services GmbH