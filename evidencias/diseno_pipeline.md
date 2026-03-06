# Diseño Pipeline
## Identificar flujo de datos
### Entrar al contenedor de postgreSQL
```
docker exec -it postgres.db psql -U user -d odoo
```
```
\pset border 0
\pset format unaligned
\df
```
```
List of functions
Schema|Name|Result data type|Argument data types|Type
public|gin_extract_query_trgm|internal|text, internal, smallint, internal, internal, internal, internal|func
public|gin_extract_value_trgm|internal|text, internal|func
public|gin_trgm_consistent|boolean|internal, smallint, text, integer, internal, internal, internal, internal|func
public|gin_trgm_triconsistent|"char"|internal, smallint, text, integer, internal, internal, internal|func
public|gtrgm_compress|internal|internal|func
public|gtrgm_consistent|boolean|internal, text, smallint, oid, internal|func
public|gtrgm_decompress|internal|internal|func
public|gtrgm_distance|double precision|internal, text, smallint, oid, internal|func
public|gtrgm_in|gtrgm|cstring|func
public|gtrgm_options|void|internal|func
public|gtrgm_out|cstring|gtrgm|func
public|gtrgm_penalty|internal|internal, internal, internal|func
public|gtrgm_picksplit|internal|internal, internal|func
public|gtrgm_same|internal|gtrgm, gtrgm, internal|func
public|gtrgm_union|gtrgm|internal, internal|func
public|set_limit|real|real|func
public|show_limit|real||func
--More--
```
### Explorar tablas
##### Tablas relevantes
```
\dt sale*
\dt res*
\dt product*
```
```
\dt *sale*
```
```
Schema|Name|Type|Owner
public|account_tax_sale_order_discount_rel|table|user
public|account_tax_sale_order_line_rel|table|user
public|product_document_sale_pdf_form_field_rel|table|user
public|product_template_attribute_value_sale_order_line_rel|table|user
public|quotation_document_sale_order_rel|table|user
public|quotation_document_sale_pdf_form_field_rel|table|user
public|sale_advance_payment_inv|table|user
public|sale_advance_payment_inv_sale_order_rel|table|user
public|sale_mass_cancel_orders|table|user
public|sale_order|table|user
public|sale_order_cancel|table|user
public|sale_order_discount|table|user
public|sale_order_line|table|user
public|sale_order_line_invoice_rel|table|user
public|sale_order_line_product_document_rel|table|user
public|sale_order_mass_cancel_wizard_rel|table|user
public|sale_order_option|table|user
public|sale_order_tag_rel|table|user
public|sale_order_template|table|user
public|sale_order_template_line|table|user
public|sale_order_template_option|table|user
public|sale_order_transaction_rel|table|user
public|sale_payment_provider_onboarding_wizard|table|user
public|sale_pdf_form_field|table|user
(24 rows)
```
```
odoo=# \dt res*
```
```
List of relations
Schema|Name|Type|Owner
public|res_bank|table|user
public|res_company|table|user
public|res_company_users_rel|table|user
public|res_config|table|user
public|res_config_settings|table|user
public|res_country|table|user
public|res_country_group|table|user
public|res_country_group_pricelist_rel|table|user
public|res_country_res_country_group_rel|table|user
public|res_country_state|table|user
public|res_currency|table|user
public|res_currency_rate|table|user
public|res_device_log|table|user
public|res_groups|table|user
public|res_groups_implied_rel|table|user
public|res_groups_report_rel|table|user
public|res_groups_spreadsheet_dashboard_rel|table|user
--More--
```
```
\dt product*
```
```
List of relations
Schema|Name|Type|Owner
public|product_attr_exclusion_value_ids_rel|table|user
public|product_attribute|table|user
public|product_attribute_custom_value|table|user
public|product_attribute_product_template_rel|table|user
public|product_attribute_value|table|user
public|product_attribute_value_product_template_attribute_line_rel|table|user
public|product_category|table|user
public|product_combo|table|user
public|product_combo_item|table|user
public|product_combo_product_template_rel|table|user
public|product_document|table|user
public|product_document_sale_pdf_form_field_rel|table|user
public|product_label_layout|table|user
public|product_label_layout_product_product_rel|table|user
public|product_label_layout_product_template_rel|table|user
public|product_optional_rel|table|user
public|product_packaging|table|user
--More--
```

## Ver estructura de sale_order
```
Table "public.sale_order"
Column|Type|Collation|Nullable|Default
id|integer||not null|nextval('sale_order_id_seq'::regclass)
campaign_id|integer|||
source_id|integer|||
medium_id|integer|||
company_id|integer||not null|
partner_id|integer||not null|
journal_id|integer|||
partner_invoice_id|integer||not null|
partner_shipping_id|integer||not null|
fiscal_position_id|integer|||
payment_term_id|integer|||
pricelist_id|integer|||
currency_id|integer|||
user_id|integer|||
team_id|integer|||
create_uid|integer|||
write_uid|integer|||
--More--
```
```
\d sale_order_line
```
```
Table "public.sale_order_line"
Column|Type|Collation|Nullable|Default
id|integer||not null|nextval('sale_order_line_id_seq'::regclass)
order_id|integer||not null|
sequence|integer|||
company_id|integer|||
currency_id|integer|||
order_partner_id|integer|||
salesman_id|integer|||
product_id|integer|||
product_uom|integer|||
linked_line_id|integer|||
combo_item_id|integer|||
product_packaging_id|integer|||
create_uid|integer|||
write_uid|integer|||
state|character varying|||
display_type|character varying|||
virtual_id|character varying|||
--More--
```
### Datos disponibles
```
SELECT id, name, partner_id, date_order, amount_total, state FROM sale_order LIMIT 10;
```
```
id|name|partner_id|date_order|amount_total|state
1|S00001|10|2026-02-05 13:13:00|1740.00|draft
2|S00002|12|2026-02-05 13:13:00|2947.50|draft
3|S00003|12|2026-03-05 13:13:45|377.50|draft
5|S00005|10|2026-02-05 13:13:00|405.00|draft
19|S00019|8|2026-02-05 13:13:00|1740.00|sent
6|S00006|16|2026-03-05 13:13:46|750.00|sale
8|S00008|11|2026-03-05 13:13:46|462.00|sale
9|S00009|11|2026-02-26 13:13:46.121647|654.00|sale
11|S00011|11|2026-02-12 13:13:46.123503|1096.50|sale
13|S00013|11|2026-03-05 13:13:46|415.50|sale
```
```
SELECT id, order_id, product_id, name, product_uom_qty, price_unit, price_subtotal FROM sale_order_line LIMIT 10;
```
```
id|order_id|product_id|name|product_uom_qty|price_unit|price_subtotal
1|1|32|[FURN_6667] Pantallas de bloque acústico (Madera)|3.00|295.00|885.00
2|1|6|[FURN_8888] Lámpara de oficina|5.00|145.00|725.00
3|1|5|[FURN_7777] Silla de oficina|2.00|65.00|130.00
4|2|3|Diseño interior virtual|24.00|75.00|1800.00
5|2|4|Área de casa virtual|30.00|38.25|1147.50
6|3|3|Diseño interior virtual|10.00|30.75|307.50
7|3|5|[FURN_7777] Silla de oficina|1.00|70.00|70.00
12|5|6|[FURN_8888] Lámpara de oficina|1.00|405.00|405.00
40|19|32|[FURN_6667] Pantallas de bloque acústico (Madera)|3.00|295.00|885.00
41|19|6|[FURN_8888] Lámpara de oficina|5.00|145.00|725.00
```

