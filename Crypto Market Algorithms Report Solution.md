```sql
SELECT 
    Q1.Algorithm, 
    Q1.V AS Q1_Volume, 
    Q2.V AS Q2_Volume, 
    Q3.V AS Q3_Volume, 
    Q4.V AS Q4_Volume 
FROM 
    (
        SELECT 
            C.Algorithm, 
            SUM(Volume) AS V 
        FROM 
            coins C 
            INNER JOIN transactions T ON T.coin_code = C.code 
        WHERE 
            YEAR(Dt) = 2020 
            AND QUARTER(Dt) = 1 
        GROUP BY 
            C.Algorithm
    ) Q1 
    INNER JOIN 
    (
        SELECT 
            C.Algorithm, 
            SUM(Volume) AS V 
        FROM 
            coins C 
            INNER JOIN transactions T ON T.coin_code = C.code 
        WHERE 
            YEAR(Dt) = 2020 
            AND QUARTER(Dt) = 2 
        GROUP BY 
            C.Algorithm
    ) Q2 ON Q1.Algorithm = Q2.Algorithm 
    INNER JOIN 
    (
        SELECT 
            C.Algorithm, 
            SUM(Volume) AS V 
        FROM 
            coins C 
            INNER JOIN transactions T ON T.coin_code = C.code 
        WHERE 
            YEAR(Dt) = 2020 
            AND QUARTER(Dt) = 3 
        GROUP BY 
            C.Algorithm
    ) Q3 ON Q1.Algorithm = Q3.Algorithm 
    INNER JOIN 
    (
        SELECT 
            C.Algorithm, 
            SUM(Volume) AS V 
        FROM 
            coins C 
            INNER JOIN transactions T ON T.coin_code = C.code 
        WHERE 
            YEAR(Dt) = 2020 
            AND QUARTER(Dt) = 4 
        GROUP BY 
            C.Algorithm
    ) Q4 ON Q1.Algorithm = Q4.Algorithm 
ORDER BY 
    Q1.Algorithm ASC;


```
