# Twitch C# Wrapper for the Twitch v3 REST API

## Note:
Sadly, I don't have time to maintain this project anymore.
But do not hesitate to make a pull request if you want to fix/change something :)

## Documentation: 
https://github.com/justintv/Twitch-API

## Example:
```c#
TwitchNamedClient client = new TwitchNamedClient("michidk", "myOAuthKey", "myClientId");

client.Follow("Gronkh");

foreach (Follower follower in client.GetFollowers("michidk").List)
{
    Console.WriteLine(follower.User.Name);
}
```

## Explanation

###### Client
Currently there are three client classes:

| Class                          | Explanation                                                           |
| ------------------------------ | --------------------------------------------------------------------- |
| TwitchReadOnlyClient           | you can use this client, without a clientid or authkey                |
| TwitchAuthenticatedClient      | this client needs an auth key - use it to get the name of the authkey |
| TwitchNamedClient              | this class needs an authkey, clientid and a name                      |

if you only have the auth-key as input, you would use an AuthenticatedClient to get the username of the associated auth-key. Then you would initialize a NamedClient.

###### Example
```c#
var tempClient = new TwitchAuthenticatedClient(authKey, clientId);
string username = tempClient.GetMyChannel().Name;
client = new TwitchNamedClient(username, authKey, clientId);
```

###### OAuth Key / Client ID
Your client id is used to protect the twitch servers from spam. You can create one here:
http://www.twitch.tv/settings/connections (scroll to the bottom)

You auth key is used to authenticate you with the twitch servers. To simply generate an authkey, just put after "client_id=" your client id and visit the following link:
```
https://api.twitch.tv/kraken/oauth2/authorize?response_type=token&client_id=INSERT_YOUR_CLIENT_ID_HERE&redirect_uri=http://localhost&scope=user_read+user_blocks_edit+user_blocks_read+user_follows_edit+channel_read+channel_editor+channel_commercial+channel_stream+channel_subscriptions+user_subscriptions+channel_check_subscription+chat_login
```

You will be redirected to a url like this:
```
http://localhost/#access_token=qxxxxtnc33456quxfghmcpw211s92xgp&scope=user_read+user_blocks_edit+user_blocks_read+user_follows_edit+channel_read+channel_editor+channel_commercial+channel_stream+channel_subscriptions+user_subscriptions+channel_check_subscription+chat_login
```

There you have your oauth key: #access_token=qxxxxtnc33456quxfghmcpw211s92xgp

read more about twitch rest api authentication here:
https://github.com/justintv/Twitch-API/blob/master/authentication.md

## Dependencies
- http://restsharp.org/
- http://www.newtonsoft.com/json

## License
Used structure and some code pieces from https://github.com/gibletto

Copyright 2015 michidk

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
