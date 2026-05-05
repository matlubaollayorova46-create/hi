import os
import shutil

# Fayl turlari bo‘yicha kategoriyalar
FILE_CATEGORIES = {
    "Images": [".jpg", ".jpeg", ".png", ".gif", ".bmp"],
    "Videos": [".mp4", ".mkv", ".avi", ".mov"],
    "Documents": [".pdf", ".docx", ".doc", ".txt", ".xlsx"],
    "Music": [".mp3", ".wav"],
    "Archives": [".zip", ".rar", ".tar", ".gz"]
}

def create_folders(base_path):
    for folder in FILE_CATEGORIES.keys():
        folder_path = os.path.join(base_path, folder)
        if not os.path.exists(folder_path):
            os.makedirs(folder_path)

def get_category(file_extension):
    for category, extensions in FILE_CATEGORIES.items():
        if file_extension.lower() in extensions:
            return category
    return "Others"

def organize_files(base_path):
    create_folders(base_path)

    for file in os.listdir(base_path):
        file_path = os.path.join(base_path, file)

        if os.path.isfile(file_path):
            _, ext = os.path.splitext(file)
            category = get_category(ext)

            target_folder = os.path.join(base_path, category)
            shutil.move(file_path, os.path.join(target_folder, file))
            print(f"{file} -> {category}")

if __name__ == "__main__":
    path = input("Papka yo‘lini kiriting: ")
    if os.path.exists(path):
        organize_files(path)
        print("Tartiblash tugadi!")
    else:
        print("Bunday papka mavjud emas.")
