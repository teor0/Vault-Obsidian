All'interno del progetto si andrà a realizzare un e-commerce e prendendo spunto da alcuni di essi (es. Amazon, ebay, ibs, ecc.) si conclude che lo schema di database sarà formato da:
- Una tabella User, che è identificato da un ID e possiede: Nome, Indirizzo, E-Mail, Password e Ruolo. In particolare il ruolo differenzia gli user in : clienti, fornitori e amministratori.
- Una tabella Prodotto, che è identificato da un ID e possiede: Nome, Categoria, Prezzo, Descrizione, Quantità. In particolare la categoria fa riferimento alla tabella Categoria Prodotto.
- Una tabella Categoria Prodotto, che è identificato da un ID e possiede: Nome.
- Una tabella Ordine, che è identificato da un ID e possiede: l'ID del cliente che lo ha effettuato, 