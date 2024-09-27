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
       
