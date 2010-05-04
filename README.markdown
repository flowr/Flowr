# Flowr Developer API v1

is a REST API for interacting with messages, flows, users and groups supports BASIC AUTH authentication. Time is in UTC format.

Errors are in format:
    { 
      'rs':2, 
      'data': [
        {
          's':SOURCE,
          'm':MESSAGE
        }
      ]
    }

## Methods

### Messages API

[GET] /api/1/messages - Reading list of Messages

    * /flowid/FLOW_ID
          o ID of flow, you can get this from flows ( default is 1 - Live flow )
          o this can also be group_id or user_id if you are fetching messages for groups or users

    * /flowtype/FLOW_TYPE
          o flow (default)
          o group
          o people

    * /time/TIME - UTC timestamp


RESPONSE:
[
   {
      "id":964,
      "user_id":20,
      "file_id":457,
      "user_name":"Vlada The Second 22",
      "user_link_url":"20-vlada-the-second-22",
      "link_url":"964-text-tag1-tag2-tag3-tag4",
      "comments_count":1,
      "likes_count":5,
      "likers":[
         {
            "id":"3",
            "fullname":"Vlada Petrovi\u0107",
            "link_url":"3-vlada-petrovi",
            "file_id":"2"
         },
         {
            "id":"4",
            "fullname":"Davorin Gabrovec",
            "link_url":"4-davorin-gabrovec",
            "file_id":"445"
         },
         {
            "id":"10",
            "fullname":"Matja\u017e van der Lipu\u0161",
            "link_url":"10-matja-van-der-lipu",
            "file_id":null
         }
      ],
      "you_likes":true,
      "you_bookmarked":true,
      "message":"text #tag1 #tag2 #tag3 #tag4 #tag5 #tag6 text",
      "tags":[

      ],
      "can_edit":true,
      "can_delete":true,
      "date":"2009-12-16 20:28:05",
      "comments":[
         {
            "id":974,
            "user_id":20,
            "file_id":457,
            "user_name":"Vlada The Second 22",
            "user_link_url":"20-vlada-the-second-22",
            "link_url":"974-spuki-ha",
            "comments_count":0,
            "likes_count":0,
            "you_likes":false,
            "you_bookmarked":false,
            "message":"spuki ha ? :)",
            "tags":[

            ],
            "type":"1",
            "can_edit":true,
            "date":"2009-12-16 22:12:10"
         }
      ],
      "type":"1",
      "source_id":1
   }
]


[GET] /api/1/messagescount - count new messages
        if you don't specify TIME you will get count of all messages from flow

    * /flowid/FLOW_ID
          o ID of flow, you can get this from flows ( default is 1 - Live flow )
          o this can also be group_id or user_id if you are fetching messages for groups or users

    * /flowtype/FLOW_TYPE
          o flow (default)
          o group
          o people

    * /time/TIME - UTC timestamp


RESPONSE:
{
   "flow_id":"17",
   "flow_type":"group",
   "count":0
}


[GET] /api/1/message/id/MESSAGE_ID - Read a single Message

RESPONSE:
{
   "id":964,
   "user_id":20,
   "file_id":457,
   "user_name":"Vlada The Second 22",
   "user_link_url":"20-vlada-the-second-22",
   "link_url":"964-text-tag1-tag2-tag3-tag4",
   "comments_count":0,
   "likes_count":5,
   "likers":[
      {
         "id":"3",
         "fullname":"Vlada Petrovi\u0107",
         "link_url":"3-vlada-petrovi",
         "file_id":"2"
      },
      {
         "id":"4",
         "fullname":"Davorin Gabrovec",
         "link_url":"4-davorin-gabrovec",
         "file_id":"445"
      },
      {
         "id":"10",
         "fullname":"Matja\u017e van der Lipu\u0161",
         "link_url":"10-matja-van-der-lipu",
         "file_id":null
      }
   ],
   "you_likes":true,
   "you_bookmarked":true,
   "message":"text #tag1 #tag2 #tag3 #tag4 #tag5 #tag6 text",
   "tags":[

   ],
   "can_edit":true,
   "can_delete":true,
   "date":"2009-12-16 20:28:05",
   "comments":[

   ],
   "documents":[
      {
         "id":450,
         "title":"random-funny-hilarious-4-25-09-35.jpg",
         "type":"image\/jpeg",
         "icon":"\/getfile\/450\/s",
         "size":"85.1 KB",
         "width":"500",
         "height":"632"
      }
   ],
   "type":"1",
   "source_id":1
}


[GET] /api/1/likers/messageid/[MESSAGE_ID] - get all likers for message
    If there is no likers response is 404 Error

    * /count/NUMBER
          o Number of liker you want to get. This is top COUNT recommended likers


RESPONSE:
[
   {
      "id":"3",
      "fullname":"Vlada Petrovi\u0107",
      "link_url":"3-vlada-petrovi",
      "file_id":"2",
      "position":"KING",
      "followers_count":0
   },
   {
      "id":"4",
      "fullname":"Davorin Gabrovec",
      "link_url":"4-davorin-gabrovec",
      "file_id":"445",
      "position":"KING",
      "followers_count":0
   }
]


[GET] /api/1/comments/messageid/[MESSAGE_ID] - get all comments for message
    If there is no comments response is 404 Error

RESPONSE:
[
   {
      "id":651,
      "user_id":4,
      "file_id":445,
      "user_name":"Davorin Gabrovec",
      "user_link_url":"4-davorin-gabrovec",
      "link_url":"651-fsdgsd",
      "comments_count":0,
      "likes_count":0,
      "you_likes":false,
      "you_bookmarked":false,
      "message":"fsdgsd",
      "tags":[

      ],
      "type":1,
      "can_edit":false,
      "can_delete":true,
      "date":"2009-12-02 15:58:18"
   }
]



[POST] /api/1/message - Creating New Messages

    * text
    * share_type [OPTIONAL]
          o 1 - group
          o 2 - user
    * share_source_id [OPTIONAL]
      id for user or group
    * url [OPTIONAL]

If you use share_type parameter share_source_id is required !


RESPONSE IS MESSAGE ( like in GET )

[POST] /api/1/comment/id/MESSAGE_ID - Comment message

    * title


RESPONSE IS BOOL

[DELETE] /api/1/message/id/MESSAGE_ID - Destroy an existing message

RESPONSE IS MESSAGE ( like in GET )

[POST] /api/1/like - Like message

    * id - message id


RESPONSE IS BOOL

[POST] /api/1/unlike - Unlike message

    * id - message id


RESPONSE IS BOOL

[POST] /api/1/bookmark - Bookmark message

    * id - message id


RESPONSE IS BOOL

[POST] /api/1/unbookmark - Unbookmark message

    * id - message id


RESPONSE IS BOOL

Flows API

[GET] /api/1/flows - Get flows for current user

RESPONSE:
[
   {
      "id":"2",
      "link_url":"company",
      "title":"Company flow",
      "hidden":false,
      "expanded":false,
      "is_group":false
   }
]

Group API

[GET] /api/1/groups - Get list of all groups

RESPONSE:
[{
   "id":20,
   "file_id":0,
   "owner":20,
   "type":1,
   "status":0,
   "is_archived":false,
   "link_url":"20-one-more-test",
   "title":"One more Test",
   "description":"test",
   "members_count":2,
   "tags":[
      "ontology",
      "tag",
      "web"
   ],
   "is_member":true,
   "is_pending":false,
   "rating":null
}]


[GET] /api/1/group/id/GROUP_ID - Get details for one group

RESPONSE:
{
   "id":20,
   "file_id":0,
   "owner":20,
   "type":1,
   "status":0,
   "is_archived":false,
   "link_url":"20-one-more-test",
   "title":"One more Test",
   "description":"test",
   "members_count":2,
   "tags":[
      "ontology",
      "tag",
      "web"
   ],
   "is_member":true,
   "is_pending":false,
   "rating":null
}


[GET] /api/1/group/members/GROUP_ID - Get members for this group

RESPONSE:
[
   {
      "id":20,
      "link_url":"20-vlada-the-second-22",
      "file_id":457,
      "title":"Vlada The Second 22",
      "position":"KING",
      "followers_count":0,
      "is_following":false,
      "last_login":"2010-03-01 19:36:07",
      "simple_info":"this is me",
      "location":"Ptuj",
      "email":"vlada@theflowr.com",
      "mobile":"2002",
      "linked_in":"http:\/\/vladapetrovic",
      "twitter":"vladapetrovic",
      "skype":"vladap",
      "tags":[
         "haha",
         "ontology",
         "tag1",
         "tag2",
         "test",
         "web"
      ],
      "expertise":[
         "dribling",
         "expertlevel2",
         "joy"
      ],
      "interests":[
         "books"
      ],
      "hobbies":[
         "sleeping"
      ],
      "is_online":true
   }
]


[GET] /api/1/join/id/GROUP_ID - Join group

RESPONSE IS BOOL

[GET] /api/1/leave/id/GROUP_ID - Leave group

RESPONSE IS BOOL

Users API

[GET] /api/1/users - Get list of all users

RESPONSE: 
[
  {
   "id":20,
   "link_url":"20-vlada-the-second-22",
   "file_id":457,
   "title":"Vlada The Second 22",
   "position":"KING",
   "followers_count":0,
   "is_following":false,
   "last_login":"2010-02-03 08:39:14",
   "simple_info":"this is me",
   "location":null,
   "email":"vlada1@theflowr.com",
   "mobile":null,
   "linked_in":null,
   "twitter":null,
   "skype":null,
   "tags":[
      "atag",
      "ideja",
      "tag1",
      "tag2",
      "tags",
      "ztag",
      "\u010dtag",
      "\u0161tag"
   ],
   "expertise":[
      "234_",
      "4asd",
      "ajsgd",
      "asd"
   ],
   "interests":null,
   "hobbies":null
   }
]

[GET] /api/1/user/id/USER_ID - Get user profile

If you don't specify user_id you get data for current user.

RESPONSE: 
{
   "id":20,
   "link_url":"20-vlada-the-second-22",
   "file_id":457,
   "title":"Vlada The Second 22",
   "position":"KING",
   "followers_count":0,
   "is_following":false,
   "last_login":"2010-02-03 08:39:14",
   "simple_info":"this is me",
   "location":null,
   "email":"vlada1@theflowr.com",
   "mobile":null,
   "linked_in":null,
   "twitter":null,
   "skype":null,
   "tags":[
      "atag",
      "ideja",
      "tag1",
      "tag2",
      "tags",
      "ztag",
      "\u010dtag",
      "\u0161tag"
   ],
   "expertise":[
      "234_",
      "4asd",
      "ajsgd",
      "asd"
   ],
   "interests":null,
   "hobbies":null
}

[GET] /api/1/follow/id/USER_ID - Follow user

RESPONSE IS BOOL

[GET] /api/1/unfollow/id/USER_ID - Unfollow user

RESPONSE IS BOOL

Profile images
You access images through web site not API.
Access point are methods 

    * /getfile/avatar/FILE_ID/SIZE
    * /getfile/group/FILE_ID/SIZE


FILE_ID - This is file_id parameter from group info or user info
SIZE - can be

    * s - 25px x 25px
    * m - 50px x 50px (default)
    * l - 100px x 100px



# Command Line Usage
get flows:
    curl -X GET -v --basic -u "user@theflowr.com:pass" http://flowr/api/1/flows

post message to everyone:
    curl -X POST -d text="this is test API call" -v --basic -u "user@theflowr.com:pass" http://flowr/api/1/message

post message to group:
    curl -X POST -d "text=this is test API call&share_type=1&share_source_id=16" -v --basic -u "user@theflowr.com:pass" http://flowr/api/1/message

post message to user:
    curl -X POST -d "text=this is test API call&share_type=2&share_source_id=2" -v --basic -u "user@theflowr.com:pass" http://flowr/api/1/message

delete message:
    curl -X DELETE -v --basic -u "user@theflowr.com:pass" http://flowr/api/1/message/id/MESSAGE_ID
