---
layout: post
title:  "First Post"
description: An example post which shows code rendering.
date:   2020-03-30 10:15:36 +000
categories: test CPP code
---
this was the first post from the template. i will keep this to remind me how to write a post with code rendering.  Maybe i will use it to render arduino or C++ code.

```cpp
char StrContains(char *str, char *sfind)
{
  char found = 0;
  char index = 0;
  char len;

  len = strlen(str);

  if (strlen(sfind) > len)
  {
    return 0;
  }
  while (index < len)
  {
    if (str[index] == sfind[found])
    {
      found++;
      if (strlen(sfind) == found)
      {
        return 1;
      }
    }
    else
    {
      found = 0;
    }
    index++;
  }
  return 0;
}
```

This rendered quite nicely!
