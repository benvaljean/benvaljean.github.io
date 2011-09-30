---
layout: post 
title: Group by day week or month (PostgreSQL)
---

Sum counts of an occurrence into days, weeks, or months

#### Group by day

    SELECT date_trunc('day', loggedin) AS "Day" , count(*) AS "No. of users"
    FROM logins
    WHERE created > now() - interval '3 months' 
    GROUP BY 1 
    ORDER BY 1;

#### Group by week

    SELECT date_trunc('week', loggedin) AS "Week" , count(*) AS "No. of users"
    FROM logins
    WHERE created > now() - interval '3 months' 
    GROUP BY 1
    ORDER BY 1;

#### Group by month

    SELECT date_trunc('month', loggedin) AS "Month" , count(*) AS "No. of users"
    FROM logins
    WHERE created > now() - interval '1 year' 
    GROUP BY 1
    ORDER BY 1;

[Category:PostgreSQL](Category:PostgreSQL "wikilink")
