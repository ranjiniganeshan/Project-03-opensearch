## log into ec2 system and execute the below commands to push logs from logstash to openseaerch

```
wget https://artifacts.elastic.co/downloads/logstash/logstash-8.12.0-linux-x86_64.tar.gz /tmp
sudo amazon-linux-extras -y install java-openjdk11


mkdir -p /usr/share/logstash
tar -xzvf /tmp/logstash-8.12.0-linux-x86_64.tar.gz -C /usr/share/logstash/
/usr/share/logstash/logstash-8.12.0/bin/logstash-plugin install logstash-output-opensearch logstash-es-output
mkdir -p /etc/logstash/conf.d
vi logstash.conf
input {
    file {
        path => "/var/log/*.log"
        start_position => "beginning"
    }
}
output {
    opensearch {
        hosts => ["https://search-cloud-es-zlm2sr2lwdccexbv4lx5hgqzma.us-west-2.es.amazonaws.com:443"]
        index => "production-logs-%{+YYYY.MM.dd}"
        user => "clouduser"
        password => "Welcome@123$"
    }
}

```
/usr/share/logstash/logstash-8.12.0/bin/logstash -f /etc/logstash/conf.d/logstash.conf













