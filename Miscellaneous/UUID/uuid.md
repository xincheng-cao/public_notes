### UUID for identifying sensitive information, like ID card number, personal address, personal phone.

- UUIDs are a sequence of randomly generated numbers so it doesn’t give out much information even if the information is leaked.

- UUID is a 128-bit number. Using int as pk but, keeping UUID as well. 

- UUID v3 v5 reproductive and irreversible 

- collision: create base ns and separate namespaces for addr, id, phone, etc

### Design namespace for UUID

`ns_dns = '6ba7b810-9dad-11d1-80b4-00c04fd430c8'`

`ns_base = uuidv5(ns_dns, 'derbysoft.com')`

`ns_addr = uuidv5( ns_base, 'bps.ddd.bi.addr');`

`ns_phone = uuidv5( ns_base, 'bps.ddd.bi.phone');`

`ns_id = uuidv5( ns_base, 'bps.ddd.bi.id');`

### reference 

[What is name and namespace?](https://stackoverflow.com/questions/10867405/generating-v5-uuid-what-is-name-and-namespace)

[Best practices on primary key, auto-increment, and UUID in RDBMs and SQL databases](https://stackoverflow.com/questions/52414414/best-practices-on-primary-key-auto-increment-and-uuid-in-rdbms-and-sql-databas)

[simp intro](https://www.scaleyourapp.com/uuid-guid-oversimplified-are-they-really-unique/)