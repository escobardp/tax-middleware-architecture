# Electronic Invoice Flow – Mexico (SAT via PAC)

## Overview

Este flujo describe el proceso de emisión de factura electrónica (CFDI) desde SAP hacia el SAT (México), utilizando un Proveedor Autorizado de Certificación (PAC), como intermediario obligatorio.

---

## Step-by-Step Flow

1. **Invoice Creation (SAP ERP)**  
   Se genera una factura en SAP, iniciando el proceso de integración.

2. **Data Extraction (Middleware)**  
   El middleware recibe los datos relevantes (cliente, impuestos, conceptos, etc.).

3. **Transformation**  
   Se transforman los datos al formato CFDI requerido por la normativa mexicana (XML estructurado).

4. **Validation**  
   Validaciones fiscales:
   - RFC válido  
   - Uso de CFDI  
   - Régimen fiscal  
   - Reglas del SAT  

5. **Routing**  
   El middleware identifica que el destino es México y deriva al **Adapter México**.

6. **Adapter Processing**  
   El adapter prepara la request específica para el PAC, incluyendo certificados digitales (CSD).

7. **Communication with PAC (e.g., Edicom)**  
   Se envía la factura al PAC para su validación y certificación.

8. **PAC Processing (Timbrado)**  
   El PAC:
   - Valida la estructura del CFDI  
   - Genera el UUID (folio fiscal)  
   - Firma digitalmente el comprobante  
   - Notifica al SAT  

9. **Response Handling**  
   El PAC retorna:
   - CFDI timbrado (válido)  
   - Rechazo (con errores)

10. **Logging & Monitoring**  
    Registro completo de la transacción.

11. **Error Handling**  
    Manejo de errores:
    - Validaciones fallidas  
    - Problemas de certificación  
    - Errores de comunicación  

---

## Key Differences vs Other Countries

- Uso obligatorio de PAC  
- Generación de UUID (timbrado)  
- Validaciones fiscales más estrictas  
- Dependencia de certificados digitales  

---

## Key Considerations

- Gestión de certificados (CSD)  
- Versionado de CFDI (3.3, 4.0, etc.)  
- Alta complejidad normativa  
- Trazabilidad completa  

---

## Outcome

- CFDI válido con UUID  
- Cumplimiento con SAT  
- Integración robusta y escalable
