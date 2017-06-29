$.ajax\({

type: 'GET', url: '999.php', data: {uname:'Tom', age: 20}, beforeSend: function\(\){ console.log\('\nbefore send....'\); console.log\(arguments\); }, success: function\(\){ console.log\('\nsuccess....'\); console.log\(arguments\); }, error: function\(\){ console.log\('\nerror....'\); console.log\(arguments\); }, complete: function\(\){ console.log\('\ncomplete....'\); console.log\(arguments\); } }\);

