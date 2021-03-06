
# Zero

```python
import rbnf.zero as ze
ze_exp = ze.compile(rbnf_src_code)
print(ze_exp.match(text))
```

A vivid example with practical factors is presented [here](https://github.com/thautwarm/RBNF/blob/master/tests/zero_module.py), which aims to give out the coefs of any polynomials.

## Sample 1

```python
import rbnf.zero as ze

ze_exp = ze.compile(
"""
pyimport rbnf.std.common.[recover_codes]
url_suffix ::= '.cn' | '.com' | '.net' | '.io'
url ::= ('https' | 'http') as _1 '://' as _2 (~url_suffix)+ as _3 url_suffix as _4
        rewrite
            recover_codes([_1, _2, *_3, _4.item])
            
text ::= (url | ~url)+ as urls
        rewrite
            tuple(url for url in urls if isinstance(url, str))
""")
text = """
<html lang="en">
  <head>
    <meta charset="utf-8">
  <link rel="dns-prefetch" href="https://assets-cdn.github.com">
  <link rel="dns-prefetch" href="https://avatars0.githubusercontent.com">
  <link rel="dns-prefetch" href="https://avatars1.githubusercontent.com">
  <link rel="dns-prefetch" href="https://avatars2.githubusercontent.com">
  <link rel="dns-prefetch" href="https://avatars3.githubusercontent.com">
  <link rel="dns-prefetch" href="https://github-cloud.s3.amazonaws.com">
  <link rel="dns-prefetch" href="https://user-images.githubusercontent.com/">

  <link crossorigin="anonymous" media="all" integrity="sha512-PkbtxdWDpLChpxtWQ0KbvJoef4XMYPq5pfd/ZmylYZTzXYpCfGwN9d+bsSKcmOJLwTkfjFkfj5wz3poDrhJoSQ==" rel="stylesheet" href="https://assets-cdn.github.com/assets/frameworks-f6e6ce21346c0d2eb22def1e8534afcb.css" />
  <link crossorigin="anonymous" media="all" integrity="sha512-LHNZGPA72iEyT2UIFOpxTPnfDcJ1Ecx8MKZgMzCJzkqfID/5niECnSBbRtDc4LDgbI3YDHu5dgs5mQiMmum6cA==" rel="stylesheet" href="https://assets-cdn.github.com/assets/github-caf1b1f61473986b3fdfa6e73e76a94f.css" />

  <meta name="viewport" content="width=device-width">
....
"""
result = ze_exp.match(text).result
print(result)
```

output: 
```
('https://assets-cdn.github.com', 'https://avatars0.githubusercontent.com', 'https://avatars1.githubusercontent.com', 'https://avatars2.githubusercontent.com', 'https://avatars3.githubusercontent.com', 'https://github-cloud.s3.amazonaws.com', 'https://user-images.githubusercontent.com', 'https://assets-cdn.github.com', 'https://assets-cdn.github.com')

```
