                página.lista de classes.remover('ativo');
            });
            
            // Mostrar página selecionada
            documento.obterElementoPorId(ID da página).lista de classes.adicionar('ativo');
            
            // Atualizar navegação
            documento.querySelectorAll('.nav-link').para cada(link => {
                link.lista de classes.remover('texto-roxo-600', 'fonte em negrito');
                link.lista de classes.adicionar('texto-cinza-700');
            });
            
            // Se a página de produtos estiver sendo exibida, preencha-a
            se (ID da página === 'produtos') {
                preencherProdutos();
            }
            
            // Voltar ao topo
            janela.rolar para(0, 0);
        }

        // Preencher grade de produtos
        função preencherProdutos() {
            constante grade = documento.obterElementoPorId('grade de produtos');
            constante produtos filtrados = Filtro atual === 'todos'?produtos:produtos.filtro(p => p.categoria === Filtro atual);
            
            grade.HTML interno = produtos filtrados.mapa(produto => `
                <div class="produto-cartão bg-branco arredondado-lg sombra-lg estouro-oculto cursor-ponteiro" onclick="showProductDetail('${produto.eu ia}')">
                    <div class="h-48 bg-gradiente-para-br${produto.gradiente}itens flexíveis-centralizar justificar-centralizar">
                        <div class="texto-4xl">${produto.ícone}</div>
                    </div>
                    <div class="p-4">
                        <h3 class="texto-lg fonte-semibold mb-2">${produto.nome}</h3>
                        <p class="texto-cinza-600 texto-sm mb-3">${produto.descrição}</p>
                        <div class="flex justificar-entre-itens-centro">
                            <span class="text-xl font-bold text-purple-600">R$${produto.preço.para corrigido(2).substituir('.', ',')}</span>
                            <button onclick="event.stopPropagation(); addToCart('${produto.eu ia}')" class="bg-purple-600 texto-branco px-3 py-1 arredondado hover:bg-purple-700 cores-de-transição texto-sm">
                                Comprar
                            </botão>
                        </div>
                    </div>
                </div>
            `).juntar('');
        }

        // Filtrar produtos
        função produtos de filtro(categoria) {
            Filtro atual = categoria;
            
            // Atualizar botões de filtro
            documento.querySelectorAll('.filtro-btn').para cada(btn => {
                btn.lista de classes.remover('bg-roxo-600', 'texto-branco');
                btn.lista de classes.adicionar('bg-cinza-200', 'texto-cinza-700');
            });
            
            evento.alvo.lista de classes.remover('bg-cinza-200', 'texto-cinza-700');
            evento.alvo.lista de classes.adicionar('bg-roxo-600', 'texto-branco');
            
            preencherProdutos();
        }

        // Mostrar detalhes do produto
        função mostrarDetalhes do Produto(ID do produto) {
            constante produto = produtos.encontrar(p => p.eu ia === ID do produto);
            se (!produto) retornar;
            
            constante contente = documento.obterElementoPorId('conteúdo-detalhado-do-produto');
            contente.HTML interno = `
                <div class="grade grade-cols-1 lg:grade-cols-2 lacuna-12">
                    <div class="bg-gradiente-para-br${produto.gradiente}arredondado-lg p-12 flex itens-centro justificar-centro">
                        <div class="texto-9xl">${produto.ícone}</div>
                    </div>
                    <div>
                        <h1 class="texto-4xl fonte-negrito texto-cinza-800 mb-4">${produto.nome}</h1>
                        <p class="texto-2xl texto-roxo-600 fonte-negrito mb-6">R$${produto.preço.para corrigido(2).substituir('.', ',')}</p>
                        <p class="texto-cinza-600 mb-6">${produto.Descrição completa}</p>
                        
                        <div class="espaço-y-4 mb-8">
                            <div class="flex itens-center">
                                <span class="font-semibold mr-2">Categoria:</span>
                                <span class="capitalize bg-purple-100 text-purple-800 px-3 py-1 arredondado-texto completo-sm">${produto.categoria}</span>
                            </div>
                            <div class="flex itens-center">
                                <span class="font-semibold mr-2">Disponibilidade:</span>
                                <span class="text-green-600">✅ Em estoque</span>
                            </div>
                        </div>
                        
                        <div class="flex espaço-x-4">
                            <button onclick="adicionarAoCarrinho('${produto.eu ia}')" class="bg-purple-600 texto-branco px-8 py-3 arredondado-lg hover:bg-purple-700 cores-de-transição fonte-semibold flex-1">
                                Adicionar ao Carrinho
                            </botão>
                            <button class="bg-gray-200 text-gray-700 px-8 py-3 rounded-lg hover:bg-gray-300 transition-colors font-semibold">
                                ❤️ Favoritar
                            </botão>
                        </div>
                        
                        <div class="mt-8 p-4 bg-green-50 arredondado-lg">
                            <h3 class="font-semibold text-green-800 mb-2">🚚 Entrega Grátis</h3>
                            <p class="text-green-700 text-sm">Para compras acima de R$ 200,00 na Grande São Paulo</p>
                        </div>
                    </div>
                </div>
            `;
            
            mostrarPágina('detalhes do produto');
        }

        // Adicionar ao carrinho
        função adicionar ao carrinho(ID do produto) {
            constante produto = produtos.encontrar(p => p.eu ia === ID do produto);
            se (!produto) retornar;
            
            carrinho.empurrar(produto);
            atualizarCartCount();
            
            // Mostrar mensagem de sucesso
            alerta(`${produto.nome}foi adicionado ao carrinho!`);
        }

        // Atualizar contagem do carrinho
        função atualizarCartCount(){
            documento.obterElementoPorId('contagem de carrinhos').conteúdo do texto = carrinho.comprimento;
        }

        // Inicializa a página
        documento.adicionarEventListener('DOMContentCarregado', função() {
            preencherProdutos();
        });
    </roteiro>
<roteiro>(função(){função c(){var b=um.conteúdoDocumento||um.contentWindow.documento;se(b){var d=b.criarElemento('roteiro');d.HTML interno="window.__CF$cv$params={r:'971d9beee24a346c',t:'MTc1NTY0ODAxMi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.obterElementosPorNomeDaTag('cabeça')[0].appendChild(d)}}se(documento.corpo){var um=documento.criarElemento('iframe');um.altura=1;um.largura=1;um.estilo.posição='absoluto';um.estilo.principal=0;um.estilo.esquerda=0;um.estilo.fronteira='nenhum';um.estilo.visibilidade='escondido';documento.corpo.appendChild(um);se('carregando'!==documento.estado pronto)c();outro se(janela.adicionarEventListener)documento.adicionarEventListener('DOMContentCarregado',c);outro{var e=documento.onreadystatechange||função(){};documento.onreadystatechange=função(b){e(b);'carregando'!==documento.estado pronto&&(documento.onreadystatechange=e,c())}}}})();</roteiro></corpo>
</HTML>

