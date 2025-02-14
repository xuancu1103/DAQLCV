Mô tả dự án
Ứng dụng giúp người dùng tạo, quản lý và theo dõi danh sách công việc hàng ngày.

Tính năng chính
Đăng ký / Đăng nhập (Firebase Authentication hoặc JWT)
Tạo, chỉnh sửa, xóa công việc
Đánh dấu hoàn thành / chưa hoàn thành
Sắp xếp công việc theo mức độ ưu tiên hoặc ngày hết hạn
Thông báo nhắc nhở (Notifications)

CODE: 
import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Card, CardContent } from "@/components/ui/card";
import { Check, Trash2 } from "lucide-react";

export default function TaskManager() {
  const [tasks, setTasks] = useState([
    { id: 1, text: "Học React", completed: false },
    { id: 2, text: "Làm bài tập lập trình", completed: true },
  ]);
  const [newTask, setNewTask] = useState("");

  const addTask = () => {
    if (newTask.trim() === "") return;
    const task = { id: Date.now(), text: newTask, completed: false };
    setTasks([...tasks, task]);
    setNewTask("");
  };

  const toggleTask = (id) => {
    setTasks(tasks.map(task => task.id === id ? { ...task, completed: !task.completed } : task));
  };

  const deleteTask = (id) => {
    setTasks(tasks.filter(task => task.id !== id));
  };

  return (
    <div className="max-w-lg mx-auto p-4">
      <h1 className="text-2xl font-bold mb-4">QLCV</h1>
      <div className="flex gap-2 mb-4">
        <Input value={newTask} onChange={(e) => setNewTask(e.target.value)} placeholder="Nhập công việc mới..." />
        <Button onClick={addTask}>Thêm</Button>
      </div>
      <div className="space-y-2">
        {tasks.map(task => (
          <Card key={task.id} className="p-2 flex items-center justify-between">
            <span className={task.completed ? "line-through text-gray-500" : ""}>{task.text}</span>
            <div className="flex gap-2">
              <Button size="icon" onClick={() => toggleTask(task.id)}>
                <Check className="w-4 h-4 text-green-500" />
              </Button>
              <Button size="icon" variant="destructive" onClick={() => deleteTask(task.id)}>
                <Trash2 className="w-4 h-4 text-red-500" />
              </Button>
            </div>
          </Card>
        ))}
      </div>
    </div>
  );
}
