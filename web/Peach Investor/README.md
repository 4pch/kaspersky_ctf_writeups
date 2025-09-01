# Writeup 1

https://gist.github.com/as3617/847b23be47633b9e626bc404458deef6


# Writeup 2

Author's solution for Peach Investor involved uploading a poisoned module to the __pycache__ and then hanging the celery with a little DoS (adding many data sources at a time). This way the celery will scale the workers and load the poisoned module.
