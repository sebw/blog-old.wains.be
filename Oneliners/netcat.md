# Netcat oneliners

#### Notification when port becomes accessible
`while ! nc -vz localhost 3306 2> /dev/null; do sleep 1; done && echo 'Database is available'`
