<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React Fundamentals: Exercises 1-4</title>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <style>
        body { font-family: sans-serif; padding: 20px; line-height: 1.6; }
        section { border-bottom: 1px solid #ddd; padding: 20px 0; }
        input { padding: 8px; margin-right: 10px; }
        button { padding: 8px 15px; cursor: pointer; }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect } = React;

        function ReactExercises() {
            // State for Exercise 1, 2, & 3
            const [students, setStudents] = useState([
                { id: 1, name: "Alice" },
                { id: 2, name: "Bob" },
                { id: 3, name: "Charlie" },
                { id: 4, name: "David" },
                { id: 5, name: "Eve" }
            ]);
            const [newName, setNewName] = useState("");

            // State for Exercise 4 (API)
            const [apiUsers, setApiUsers] = useState([]);

            // Handle Add Student (Exercise 3)
            const handleAddStudent = (e) => {
                e.preventDefault();
                if (!newName.trim()) return;
                const newEntry = { id: Date.now(), name: newName };
                setStudents([...students, newEntry]);
                setNewName("");
            };

            // Fetch API Data (Exercise 4)
            useEffect(() => {
                fetch('https://jsonplaceholder.typicode.com/users?_limit=3')
                    .then(res => res.json())
                    .then(data => setApiUsers(data));
            }, []);

            return (
                <div>
                    <h1>React Learning Module</h1>

                    {/* Exercise 1 & 2: List Rendering and Keys */}
                    <section>
                        <h2>Exercises 1 & 2: Student List</h2>
                        <ul>
                            {students.map(student => (
                                <li key={student.id}>{student.name}</li>
                            ))}
                        </ul>
                    </section>

                    {/* Exercise 3: Form Submit */}
                    <section>
                        <h2>Exercise 3: Add New Student</h2>
                        <form onSubmit={handleAddStudent}>
                            <input 
                                type="text" 
                                value={newName} 
                                onChange={(e) => setNewName(e.target.value)} 
                                placeholder="Enter name"
                            />
                            <button type="submit">Add Student</button>
                        </form>
                    </section>

                    {/* Exercise 4: Fetch API */}
                    <section>
                        <h2>Exercise 4: Data from Dummy API</h2>
                        <ul>
                            {apiUsers.length > 0 ? (
                                apiUsers.map(user => (
                                    <li key={user.id}>{user.name} - {user.email}</li>
                                ))
                            ) : (
                                <p>Loading API data...</p>
                            )}
                        </ul>
                    </section>
                </div>
            );
        }

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<ReactExercises />);
    </script>
</body>
</html>
