# semana16
Aplicacion de GUI con atajos y funciones especificas
import tkinter as tk
from tkinter import ttk, messagebox

# Funciones para tareas pendientes
def add_task(event=None):
    task = task_entry.get()
    if task:
        task_listbox.insert(tk.END, task)
        task_entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Advertencia", "Por favor ingresa una tarea.")

def complete_task(event=None):
    try:
        selected_task_index = task_listbox.curselection()[0]
        task = task_listbox.get(selected_task_index)
        task_listbox.delete(selected_task_index)
        task_listbox.insert(selected_task_index, f"[Completada] {task}")
    except IndexError:
        messagebox.showwarning("Advertencia", "Por favor selecciona una tarea.")

def delete_task(event=None):
    try:
        selected_task_index = task_listbox.curselection()[0]
        task_listbox.delete(selected_task_index)
    except IndexError:
        messagebox.showwarning("Advertencia", "Por favor selecciona una tarea.")

def close_app(event=None):
    root.destroy()

# Funciones para gestión de clientes
def add_client():
    client_name = client_entry.get()
    if client_name:
        client_listbox.insert(tk.END, client_name)
        client_entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Advertencia", "Por favor ingresa un nombre de cliente.")

def delete_client():
    try:
        selected_client_index = client_listbox.curselection()[0]
        client_listbox.delete(selected_client_index)
    except IndexError:
        messagebox.showwarning("Advertencia", "Por favor selecciona un cliente.")

# Funciones para gestión de productos
def add_product():
    product_name = product_entry.get()
    if product_name:
        product_listbox.insert(tk.END, product_name)
        product_entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Advertencia", "Por favor ingresa un nombre de producto.")

def delete_product():
    try:
        selected_product_index = product_listbox.curselection()[0]
        product_listbox.delete(selected_product_index)
    except IndexError:
        messagebox.showwarning("Advertencia", "Por favor selecciona un producto.")

# Configuración de la ventana principal
root = tk.Tk()
root.title("Gestión de Químicos y Envases")

# Creación de pestañas
tab_control = ttk.Notebook(root)
tasks_tab = ttk.Frame(tab_control)
clients_tab = ttk.Frame(tab_control)
products_tab = ttk.Frame(tab_control)
tab_control.add(tasks_tab, text="Tareas Pendientes")
tab_control.add(clients_tab, text="Clientes")
tab_control.add(products_tab, text="Productos")
tab_control.pack(expand=1, fill="both")

# Pestaña de Tareas Pendientes
task_entry = tk.Entry(tasks_tab, width=50)
task_entry.pack(pady=10)
task_entry.bind("<Return>", add_task)

task_listbox = tk.Listbox(tasks_tab, width=50, height=15)
task_listbox.pack(pady=10)

button_frame = tk.Frame(tasks_tab)
button_frame.pack(pady=10)

tk.Button(button_frame, text="Añadir Tarea", command=add_task).grid(row=0, column=0, padx=5)
tk.Button(button_frame, text="Completar Tarea", command=complete_task).grid(row=0, column=1, padx=5)
tk.Button(button_frame, text="Eliminar Tarea", command=delete_task).grid(row=0, column=2, padx=5)

root.bind("<c>", complete_task)
root.bind("<d>", delete_task)
root.bind("<Delete>", delete_task)
root.bind("<Escape>", close_app)

# Pestaña de Clientes
client_entry = tk.Entry(clients_tab, width=50)
client_entry.pack(pady=10)

client_listbox = tk.Listbox(clients_tab, width=50, height=15)
client_listbox.pack(pady=10)

client_button_frame = tk.Frame(clients_tab)
client_button_frame.pack(pady=10)

tk.Button(client_button_frame, text="Añadir Cliente", command=add_client).grid(row=0, column=0, padx=5)
tk.Button(client_button_frame, text="Eliminar Cliente", command=delete_client).grid(row=0, column=1, padx=5)

# Pestaña de Productos
product_entry = tk.Entry(products_tab, width=50)
product_entry.pack(pady=10)

product_listbox = tk.Listbox(products_tab, width=50, height=15)
product_listbox.pack(pady=10)

product_button_frame = tk.Frame(products_tab)
product_button_frame.pack(pady=10)

tk.Button(product_button_frame, text="Añadir Producto", command=add_product).grid(row=0, column=0, padx=5)
tk.Button(product_button_frame, text="Eliminar Producto", command=delete_product).grid(row=0, column=1, padx=5)

# Iniciar la aplicación
root.mainloop()
