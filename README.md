const { app, BrowserWindow } = require('electron/main')
const path = require('node:path')

function createWindow () {
  const win = new BrowserWindow({
    width: 700,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'main.js')
    }
  })

  win.loadFile('index.html')
} 

app.whenReady().then(() => {
  createWindow()

  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow()
    }
  })
})

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit()
  }
})

function addTask(){
  const newTask =document.createElement('li')
  const taskList = document.getElementById('taskList')
  taskList.appendChild(newTask)
  newTask.textContent = document.getElementById('inputTask').value
  document.getElementById('inputTask').value =""

  deleteTask(newTask)
}

function deleteTask(newTask)
{
  const deleteBtn =document.createElement('button')
  deleteBtn.textContent='Remove'
  newTask.appendChild(deleteBtn)
  deleteBtn.onclick = function(){
    newTask.remove() 
  }
}
