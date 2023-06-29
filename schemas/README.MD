#### Schemas and Tables

````

{"type":"record","name":"osquery.wifi_status","namespace":"org.apache.nifi","fields":[{"name":"bssid","type":["string","null"]},{"name":"channel","type":["string","null"]},{"name":"channel_band","type":["string","null"]},{"name":"channel_width","type":["string","null"]},{"name":"country_code","type":["string","null"]},{"name":"interface","type":["string","null"]},{"name":"mode","type":["string","null"]},{"name":"network_name","type":["string","null"]},{"name":"noise","type":["string","null"]},{"name":"rssi","type":["string","null"]},{"name":"security_type","type":["string","null"]},{"name":"ssid","type":["string","null"]},{"name":"transmit_rate","type":["string","null"]},{"name":"ts","type":["string","null"]},{"name":"uuid","type":["string","null"]}]}


{"type":"record","name":"osquery.system_info","namespace":"org.apache.nifi","fields":[{"name":"board_model","type":["string","null"]},{"name":"board_serial","type":["string","null"]},{"name":"board_vendor","type":["string","null"]},{"name":"board_version","type":["string","null"]},{"name":"computer_name","type":["string","null"]},{"name":"cpu_brand","type":["string","null"]},{"name":"cpu_logical_cores","type":["string","null"]},{"name":"cpu_microcode","type":["string","null"]},{"name":"cpu_physical_cores","type":["string","null"]},{"name":"cpu_subtype","type":["string","null"]},{"name":"cpu_type","type":["string","null"]},{"name":"hardware_model","type":["string","null"]},{"name":"hardware_serial","type":["string","null"]},{"name":"hardware_vendor","type":["string","null"]},{"name":"hardware_version","type":["string","null"]},{"name":"hostname","type":["string","null"]},{"name":"local_hostname","type":["string","null"]},{"name":"physical_memory","type":["string","null"]},{"name":"uuid","type":["string","null"]},{"name":"ts","type":["string","null"]}]}

{"type":"record","name":"osquery.temperature_sensors","namespace":"org.apache.nifi","fields":[{"name":"celsius","type":["string","null"]},{"name":"fahrenheit","type":["string","null"]},{"name":"key","type":["string","null"]},{"name":"name","type":["string","null"]},{"name":"ts","type":["string","null"]},{"name":"uuid","type":["string","null"]}]}

{"type":"record","name":"osquery.apps","namespace":"org.apache.nifi","fields":[{"name":"applescript_enabled","type":["string","null"]},{"name":"bundle_executable","type":["string","null"]},{"name":"bundle_identifier","type":["string","null"]},{"name":"bundle_name","type":["string","null"]},{"name":"bundle_package_type","type":["string","null"]},{"name":"bundle_short_version","type":["string","null"]},{"name":"bundle_version","type":["string","null"]},{"name":"category","type":["string","null"]},{"name":"compiler","type":["string","null"]},{"name":"copyright","type":["string","null"]},{"name":"development_region","type":["string","null"]},{"name":"display_name","type":["string","null"]},{"name":"element","type":["string","null"]},{"name":"environment","type":["string","null"]},{"name":"info_string","type":["string","null"]},{"name":"last_opened_time","type":["string","null"]},{"name":"minimum_system_version","type":["string","null"]},{"name":"name","type":["string","null"]},{"name":"path","type":["string","null"]},{"name":"ts","type":["string","null"]},{"name":"uuid","type":["string","null"]}]}


{"type":"record","name":"osquery.usb_devices","namespace":"org.apache.nifi","fields":[{"name":"class","type":["string","null"]},{"name":"model","type":["string","null"]},{"name":"model_id","type":["string","null"]},{"name":"protocol","type":["string","null"]},{"name":"removable","type":["string","null"]},{"name":"serial","type":["string","null"]},{"name":"subclass","type":["string","null"]},{"name":"usb_address","type":["string","null"]},{"name":"usb_port","type":["string","null"]},{"name":"vendor","type":["string","null"]},{"name":"vendor_id","type":["string","null"]},{"name":"version","type":["string","null"]},{"name":"ts","type":["string","null"]},{"name":"uuid","type":["string","null"]}]}


CREATE TABLE `ssb`.`Meetups`.`osqwifistatus` (
  `bssid` VARCHAR(2147483647),
  `channel` VARCHAR(2147483647),
  `channel_band` VARCHAR(2147483647),
  `channel_width` VARCHAR(2147483647),
  `country_code` VARCHAR(2147483647),
  `interface` VARCHAR(2147483647),
  `mode` VARCHAR(2147483647),
  `network_name` VARCHAR(2147483647),
  `noise` VARCHAR(2147483647),
  `rssi` VARCHAR(2147483647),
  `security_type` VARCHAR(2147483647),
  `ssid` VARCHAR(2147483647),
  `transmit_rate` VARCHAR(2147483647),
  `ts` VARCHAR(2147483647),
  `uuid` VARCHAR(2147483647),
  `eventTimestamp` TIMESTAMP(3) WITH LOCAL TIME ZONE METADATA FROM 'timestamp',
  WATERMARK FOR `eventTimestamp` AS `eventTimestamp` - INTERVAL '3' SECOND
) WITH (
  'scan.startup.mode' = 'group-offsets',
  'deserialization.failure.policy' = 'dlq',
  'properties.request.timeout.ms' = '120000',
  'properties.auto.offset.reset' = 'earliest',
  'format' = 'json',
  'properties.bootstrap.servers' = 'kafka:9092',
  'connector' = 'kafka',
  'properties.transaction.timeout.ms' = '900000',
  'topic' = 'osquery.wifi_status',
  'properties.group.id' = 'ssbwifistatusreader',
  'deserialization.failure.dlq.topic' = 'osquery.dlq'
)



CREATE TABLE `ssb`.`Meetups`.`thermalsensors` (
  `uuid` VARCHAR(2147483647),
  `ipaddress` VARCHAR(2147483647),
  `cputempf` BIGINT,
  `runtime` BIGINT,
  `host` VARCHAR(2147483647),
  `hostname` VARCHAR(2147483647),
  `macaddress` VARCHAR(2147483647),
  `endtime` VARCHAR(2147483647),
  `te` VARCHAR(2147483647),
  `cpu` DOUBLE,
  `diskusage` VARCHAR(2147483647),
  `memory` DOUBLE,
  `rowid` VARCHAR(2147483647),
  `systemtime` VARCHAR(2147483647),
  `ts` BIGINT,
  `starttime` VARCHAR(2147483647),
  `datetimestamp` VARCHAR(2147483647),
  `temperature` DOUBLE,
  `humidity` DOUBLE,
  `co2` DOUBLE,
  `equivalentco2ppm` DOUBLE,
  `totalvocppb` DOUBLE,
  `pressure` DOUBLE,
  `temperatureicp` DOUBLE,
  `eventTimeStamp` TIMESTAMP(3) WITH LOCAL TIME ZONE METADATA FROM 'timestamp',
  WATERMARK FOR `eventTimeStamp` AS `eventTimeStamp` - INTERVAL '3' SECOND
) WITH (
  'deserialization.failure.policy' = 'ignore_and_log',
  'properties.request.timeout.ms' = '120000',
  'format' = 'json',
  'properties.bootstrap.servers' = 'kafka:9092',
  'connector' = 'kafka',
  'properties.transaction.timeout.ms' = '900000',
  'topic' = 'thermalsensors',
  'scan.startup.mode' = 'group-offsets',
  'properties.auto.offset.reset' = 'earliest',
  'properties.group.id' = 'ssbtherms1'
)


CREATE TABLE `ssb`.`Meetups`.`weather1` (
  `uuid` VARCHAR(2147483647),
  `ts` BIGINT,
  `credit` VARCHAR(2147483647),
  `credit_URL` VARCHAR(2147483647),
  `image` ROW<`url` VARCHAR(2147483647), `title` VARCHAR(2147483647), `link` VARCHAR(2147483647)>,
  `suggested_pickup` VARCHAR(2147483647),
  `suggested_pickup_period` BIGINT,
  `location` VARCHAR(2147483647),
  `station_id` VARCHAR(2147483647),
  `latitude` DOUBLE,
  `longitude` DOUBLE,
  `observation_time` VARCHAR(2147483647),
  `observation_time_rfc822` VARCHAR(2147483647),
  `weather` VARCHAR(2147483647),
  `temperature_string` VARCHAR(2147483647),
  `temp_f` DOUBLE,
  `temp_c` DOUBLE,
  `relative_humidity` BIGINT,
  `wind_string` VARCHAR(2147483647),
  `wind_dir` VARCHAR(2147483647),
  `wind_degrees` BIGINT,
  `wind_mph` DOUBLE,
  `wind_kt` BIGINT,
  `pressure_in` DOUBLE,
  `dewpoint_string` VARCHAR(2147483647),
  `dewpoint_f` DOUBLE,
  `dewpoint_c` DOUBLE,
  `visibility_mi` DOUBLE,
  `icon_url_base` VARCHAR(2147483647),
  `two_day_history_url` VARCHAR(2147483647),
  `icon_url_name` VARCHAR(2147483647),
  `ob_url` VARCHAR(2147483647),
  `disclaimer_url` VARCHAR(2147483647),
  `copyright_url` VARCHAR(2147483647),
  `privacy_policy_url` VARCHAR(2147483647),
  `eventTimestamp` TIMESTAMP(3) WITH LOCAL TIME ZONE METADATA FROM 'timestamp',
  WATERMARK FOR `eventTimestamp` AS `eventTimestamp` - INTERVAL '3' SECOND
) WITH (
  'deserialization.failure.policy' = 'ignore_and_log',
  'properties.request.timeout.ms' = '120000',
  'format' = 'json',
  'properties.bootstrap.servers' = 'kafka:9092',
  'connector' = 'kafka',
  'properties.transaction.timeout.ms' = '900000',
  'topic' = 'weather',
  'scan.startup.mode' = 'group-offsets',
  'properties.auto.offset.reset' = 'earliest',
  'properties.group.id' = 'ssbweather001'
)



````
