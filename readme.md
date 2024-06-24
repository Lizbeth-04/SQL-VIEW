La tabla invoice ,product y client ya las tenemos creadas.En base a la tabla de invoice crearemos los view correcpondientes.

CREAMOS UNA TABLA QUE LLAME A LAS TABLA DE INVOICE Y PRODUCT.


CREATE TABLE IF NOT EXISTS invoice_detail (
    id SERIAL PRIMARY KEY,
    invoice_id INT,
    product_id INT,
    quantity INT,
    subtotal DECIMAL(9,2),
    FOREIGN KEY (invoice_id) REFERENCES invoice (id),
    FOREIGN KEY (product_id) REFERENCES product (id)
);

CREAMOS LOS VIEWS 


CREATE VIEW invoice_view AS
SELECT
    i.id,
    i.code,
    i.create_at,
    i.total,
    c.full_name AS fullname
FROM
    invoice i
JOIN
    client c ON i.client_id = c.id;
CREATE VIEW detail_view AS
SELECT
    d.id,
    d.quantity,
    p.description,
    p.price,
    d.subtotal`
FROM
    invoice_detail d
JOIN
    product p ON d.product_id = p.id;
