# Secrets

Configurations may be passed as secrets. All configuration variables may be passed using secrets.

#### Development

For development, only the following files need to be filled. The remaining can be created as empty files

- `ConnectionStrings__DefaultConnection` =
```
server=db;port=3306;Database=agora_database;User=agorauser;Password=agorapassword;default command timeout=120
```

- `db_name` =
```
agora_database
```

- `db_password` =
```
agorapassword
```

- `db_root_password` =
```
agorapassword_root
```

- `db_username` =
```
agorauser
```