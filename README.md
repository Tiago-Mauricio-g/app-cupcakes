# app-cupcakes
PIT 2 - Aplicativo cupcakes

from flask import Flask, render_template, request, redirect, url_for
from models import Usuario, Pedido, Cupcake, Pagamento

app = Flask(__name__)

@app.route('/')
def home():
    # Exibe cupcakes disponíveis
    cupcakes = Cupcake.query.all()
    return render_template('home.html', cupcakes=cupcakes)

@app.route('/pedido', methods=['POST'])
def criar_pedido():
    # Cria um novo pedido
    id_usuario = request.form['id_usuario']
    novo_pedido = Pedido(id_usuario=id_usuario, status='Pendente')
    db.session.add(novo_pedido)
    db.session.commit()
    return redirect(url_for('home'))

if __name__ == '__main__':
    app.run(debug=True)
