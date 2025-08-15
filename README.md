# DELIMITER
FIXED LENGTH OPTIONS 
DELIMITER //

CREATE PROCEDURE AddCustomer(
    IN cust_name VARCHAR(100),
    IN cust_email VARCHAR(100)
)
BEGIN
    IF NOT EXISTS (
        SELECT 1 FROM customers WHERE email = cust_email
    ) THEN
        INSERT INTO customers(name, email) VALUES (cust_name, cust_email);
    END IF;
END //

DELIMITER ;

CALL AddCustomer('Aarav Mehta', 'aarav@example.com');

DELIMITER //

CREATE FUNCTION CalculateDiscount(purchase DECIMAL(10,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    DECLARE discount DECIMAL(10,2);
    IF purchase >= 1000 THEN
        SET discount = purchase * 0.10;
    ELSE
        SET discount = purchase * 0.05;
    END IF;
    RETURN discount;
END //

DELIMITER ;

SELECT CalculateDiscount(1200);  -- Returns 120.00
