# Importação das bibliotecas
import matplotlib.pyplot as plt
import numpy as np

print("=" * 60)
print("MERCADINHO CABUGI - ANÁLISE DE VENDAS E LUCRATIVIDADE")
print(f"Faturamento Total 2025: R$ 100.640,00")
print(f"Lucro Total Anual: R$ 66.422,40 (66% do faturamento)")
print("=" * 60)

# ============================================================
# GRÁFICO 1 - PRODUTOS MAIS VENDIDOS (QUANTIDADE)
# ============================================================

produtos = ['Pão Francês (kg)', 'Cuscuz Santa Clara (un)', 'Arroz Tio João (un)', 
            'Carne Bovina (kg)', 'Salsicha Perdigão (kg)']
quantidades = [12450, 3250, 2875, 4820, 2398]

plt.figure(figsize=(10, 6))
cores = plt.cm.Blues(np.linspace(0.4, 0.9, len(produtos)))
bars = plt.barh(produtos, quantidades, color=cores)

plt.xlabel('Quantidade Vendida (kg ou unidades)', fontsize=12)
plt.ylabel('Produtos', fontsize=12)
plt.title('Mercadinho Cabugi - Produtos Mais Vendidos (2025)', fontsize=14, fontweight='bold')

for bar, valor in zip(bars, quantidades):
    plt.text(bar.get_width() + 200, bar.get_y() + bar.get_height()/2, 
             f'{valor:,.0f}', va='center', fontsize=10)

plt.gca().invert_yaxis()
plt.tight_layout()
plt.show()

# ============================================================
# GRÁFICO 2 - PRODUTOS COM MAIOR LUCRO TOTAL
# ============================================================

produtos_lucro = ['Carne Bovina (kg)', 'Pão Francês (kg)', 'Arroz Tio João (un)', 
                  'Salsicha Perdigão (kg)', 'Cuscuz Santa Clara (un)']
lucro_total_produtos = [19200, 9400, 6500, 5400, 3650]

plt.figure(figsize=(10, 6))
cores = plt.cm.Greens(np.linspace(0.3, 0.8, len(produtos_lucro)))
bars = plt.barh(produtos_lucro, lucro_total_produtos, color=cores)

plt.xlabel('Lucro Total (R$)', fontsize=12)
plt.ylabel('Produtos', fontsize=12)
plt.title('Mercadinho Cabugi - Produtos com Maior Lucro Total (2025)', fontsize=14, fontweight='bold')

for bar, valor in zip(bars, lucro_total_produtos):
    plt.text(bar.get_width() + 300, bar.get_y() + bar.get_height()/2, 
             f'R$ {valor:,.0f}', va='center', fontsize=10)

plt.gca().invert_yaxis()
plt.tight_layout()
plt.show()

# ============================================================
# GRÁFICO 3 - DISPERSÃO: QUANTIDADE VS LUCRO TOTAL
# ============================================================

produtos_disp = ['Pão Francês', 'Carne Bovina', 'Cuscuz Santa Clara', 
                 'Arroz Tio João', 'Salsicha Perdigão']
quantidade_disp = [12450, 4820, 3250, 2875, 2398]
lucro_disp = [9400, 19200, 3650, 6500, 5400]

plt.figure(figsize=(10, 7))
plt.scatter(quantidade_disp, lucro_disp, s=200, c='steelblue', alpha=0.7, edgecolors='darkblue', linewidth=1.5)

# Destacar produtos prioritários
plt.scatter([12450], [9400], s=300, c='orange', edgecolors='red', linewidth=2, label='Pão Francês')
plt.scatter([4820], [19200], s=300, c='darkgreen', edgecolors='black', linewidth=2, label='Carne Bovina')
plt.scatter([2875], [6500], s=300, c='gold', edgecolors='brown', linewidth=2, label='Arroz Tio João')

for i, produto in enumerate(produtos_disp):
    plt.annotate(produto, (quantidade_disp[i] + 200, lucro_disp[i] + 500), fontsize=10, ha='left')

plt.xlabel('Quantidade Vendida (kg ou unidades)', fontsize=12)
plt.ylabel('Lucro Total (R$)', fontsize=12)
plt.title('Mercadinho Cabugi - Relação Quantidade vs Lucro Total (2025)', fontsize=14, fontweight='bold')
plt.axhline(y=7000, color='gray', linestyle='--', alpha=0.5)
plt.axvline(x=4000, color='gray', linestyle='--', alpha=0.5)
plt.legend(loc='upper left')
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()

# ============================================================
# GRÁFICO 4 - EVOLUÇÃO DO FATURAMENTO MENSAL (2025)
# ============================================================

meses = ['Jan', 'Fev', 'Mar', 'Abr', 'Mai', 'Jun', 
         'Jul', 'Ago', 'Set', 'Out', 'Nov', 'Dez']
faturamento = [6450, 6720, 8100, 7350, 7580, 9820, 
               9150, 8430, 8690, 7860, 9450, 10980]

plt.figure(figsize=(12, 6))
plt.plot(meses, faturamento, marker='o', linewidth=2, markersize=8, color='darkred', label='Faturamento')
plt.fill_between(meses, faturamento, alpha=0.2, color='red')

# Destacar o pico de dezembro
plt.plot('Dez', 10980, marker='*', markersize=20, color='gold', markeredgecolor='black')

plt.xlabel('Mês', fontsize=12)
plt.ylabel('Faturamento (R$)', fontsize=12)
plt.title('Mercadinho Cabugi - Evolução do Faturamento Mensal (2025)', fontsize=14, fontweight='bold')
plt.legend()
plt.grid(True, alpha=0.3)

plt.gca().yaxis.set_major_formatter(plt.FuncFormatter(lambda x, p: f'R$ {x:,.0f}'))
plt.tight_layout()
plt.show()

# ============================================================
# GRÁFICO 5 - LUCRO TOTAL POR SETOR
# ============================================================

setores = ['Mercearia', 'Açougue', 'Padaria', 'Hortifruti', 'Limpeza']
lucro_setor = [20723.79, 19196.07, 12221.72, 8302.80, 5978.02]  # 66% de cada faturamento
cores_setor = ['#3498db', '#e74c3c', '#f39c12', '#2ecc71', '#95a5a6']

plt.figure(figsize=(10, 6))
bars = plt.bar(setores, lucro_setor, color=cores_setor, edgecolor='black', linewidth=1.5)

total_lucro = sum(lucro_setor)
for bar, valor in zip(bars, lucro_setor):
    percentual = (valor / total_lucro) * 100
    plt.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 400, 
             f'R$ {valor:,.2f}\n({percentual:.1f}%)', 
             ha='center', va='bottom', fontsize=9, fontweight='bold')

plt.ylabel('Lucro Total (R$)', fontsize=12)
plt.xlabel('Setores', fontsize=12)
plt.title('Mercadinho Cabugi - Lucro Total por Setor (2025)', fontsize=14, fontweight='bold')

plt.gca().yaxis.set_major_formatter(plt.FuncFormatter(lambda x, p: f'R$ {x:,.0f}'))
plt.ylim(0, 25000)
plt.grid(axis='y', alpha=0.3)
plt.tight_layout()
plt.show()

# ============================================================
# RESULTADOS FINAIS
# ============================================================

print("\n" + "=" * 60)
print("📊 RESULTADOS FINAIS - MERCADINHO CABUGI 2025")
print("=" * 60)
print(f"💰 Faturamento Bruto Total: R$ 100.640,00")
print(f"💰 Lucro Total (66% do faturamento): R$ 66.422,40")
print(f"🥩 Setor mais lucrativo: Açougue (R$ 19.196,07 - 28,9%)")
print(f"🥖 Produto mais vendido: Pão Francês (12.450 kg)")
print(f"💰 Produto mais lucrativo: Carne Bovina (R$ 19.200,00)")
print("=" * 60)
