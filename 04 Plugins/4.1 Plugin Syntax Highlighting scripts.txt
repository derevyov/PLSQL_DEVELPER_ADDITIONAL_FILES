https://www.allroundautomations.com/products/pl-sql-developer/plug-ins/
------------------------------
SELECT DISTINCT p.object_name
  FROM user_procedures p
UNION
SELECT q.procedure_name
  FROM user_procedures q
UNION
SELECT w.object_name || '.' || w.procedure_name
  FROM user_procedures w
-- Refresh on reconnect := true
------------------------------
SELECT DISTINCT synonym_name || '.' || procedure_name
  FROM all_procedures p, all_synonyms s
 WHERE s.table_name = p.object_name
      -- AND p.owner = 'SYS'
      -- AND s.owner = 'PUBLIC'
      -- AND p.object_name != 'STANDARD'
   AND s.SYNONYM_NAME IN ('DBMS_LOB', 'DBMS_RANDOM', 'DBMS_SQL', 'DBMS_OUTPUT', 'DBMS_UTILITY')
-- refresh on reconnect := false
------------------------------
SELECT DISTINCT object_name
  FROM all_arguments
 WHERE package_name = 'STANDARD'
   AND owner = 'SYS'
-- refresh on reconnect := false
-- style: Keywords
------------------------------
SELECT DISTINCT t.ARGUMENT_NAME 
FROM User_Arguments t 
WHERE t.ARGUMENT_NAME IS NOT NULL
-- Refresh on reconnect := true
------------------------------
SELECT s.table_name FROM user_tables s 
 UNION 
SELECT v.view_name FROM user_views v;
-- Refresh on reconnect := true