*Prompting [[Large Language Model|LLMs]] to perform classification tasks with X labeled examples.*
### Zero-Shot Example
```plaintext
Classifica os seguintes textos de acordo com o sentimento transmitido. As classes possíveis são: Positivo, Negativo, Neutro. 
o novo espaço é muito bom => [MASK]
```
### Few-Shot Example
```plaintext
Classifica os seguintes textos de acordo com o sentimento transmitido. As classes possíveis são: Positivo, Negativo, Neutro. 
ambiente muito bom => Positivo 
serviço muito mau, muito mau => Negativo 
não aquece nem arrefece => Neutro 
serviço bom, ambiente excelente => Positivo 
muito mau ambiente => Negativo 
o novo espaço é muito bom => [MASK]
```