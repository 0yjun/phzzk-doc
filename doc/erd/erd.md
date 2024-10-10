Table user { 
  id integer [primary key] 
  username varchar 
  role varchar 
  created_at timestamp 
}

Table follow { 
  id integer [primary key] 
  following_user_id integer 
  followed_user_id integer 
}

Table Block { 
  id integer [primary key] 
  blocker_user_id integer 
  blocked_user_id integer 
}

Table stream { 
  id integer [primary key] 
  user_id integer 
}

Table video { 
  id uuid [primary key] 
  stream_id integer 
}

Table chat { 
  id integer [primary key] 
  stream_id integer 
  user_id integer 
  message text 
  timestamp timestamp 
}

Table manager { 
  id integer [primary key] 
  streamer_id integer 
  manager_id integer 
}
Ref: "user"."id" < "follow"."following_user_id"
Ref: "user"."id" < "follow"."followed_user_id"
Ref: "user"."id" < "Block"."blocker_user_id"
Ref: "user"."id" < "Block"."blocked_user_id"
Ref: "user"."id" < "stream"."user_id"
Ref: "stream"."id" < "video"."stream_id"
Ref: "user"."id" < "chat"."user_id"
Ref: "stream"."id" < "chat"."stream_id"
Ref: "user"."id" < "manager"."streamer_id"
Ref: "user"."id" < "manager"."manager_id"
