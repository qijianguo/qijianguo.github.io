﻿---
title: Springboot自定义分页工具类
categories: SpringBoot
tags: springboot
date: 2018-07-07 21:35:21
---

<!-- more -->

```

import org.springframework.data.domain.Page;
import org.springframework.data.domain.PageImpl;
import org.springframework.data.domain.PageRequest;

import java.util.List;

public class PageUtil {
    /**
     * 分页
     * @param list
     * @param page
     * @param pageSize
     * @param <T>
     * @return
     */
    public static <T> Page<T> page(List<T> list, int page, int pageSize) {
        int totalElements = list.size();
        int start = page * pageSize;
        int end = Math.min(start + pageSize, totalElements);

        return new PageImpl<>(list.subList(start, end),
                new PageRequest(page, pageSize),
                totalElements);
    }

    public static <T> Page<T> builidPage(List<T> list, long totalElements, int page, int pageSize) {
        return new PageImpl<>(list,
                new PageRequest(page, pageSize),
                totalElements);
    }

}

```
pom.xml
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

