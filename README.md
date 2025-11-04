from PIL import Image, ImageDraw, ImageFont
import os, textwrap, random, math
os.makedirs("/mnt/data/thumbnails", exist_ok=True)

def draw_matrix_thumb(filename, title, subtitle, accent="#00ff66", size=(640,320)):
    w,h = size
    img = Image.new("RGBA", size, (1,1,1,255))
    draw = ImageDraw.Draw(img)

    # Background gradient
    for y in range(h):
        t = y / h
        r = int(1 + (0 - 1) * t)
        g = int(2 + (34 - 2) * t)
        b = int(1 + (1 - 1) * t)
        draw.line([(0,y),(w,y)], fill=(r,g,b))
    # Add semi-transparent glow
    glow = Image.new("RGBA", size, (0,40,0,40))
    img = Image.alpha_composite(img, glow)

    # Draw matrix rain columns (binary and katakana-like)
    cols = 12
    for c in range(cols):
        x = int((w/cols)*c + random.randint(-10,10))
        y_start = random.randint(-300, -20)
        speed = random.uniform(0.6, 1.4)
        y = y_start
        chs = ["01","10","11","00","ﾛ","ﾊ","ﾐ","ﾅ","ﾓ","ｴ","ｵ","ｲ","ﾊ","ｱ","ﾘ"]
        for i in range(30):
            # vary opacity and size
            op = int(40 + (i*6))
            font_size = int(10 + (i*0.6))
            try:
                font = ImageFont.truetype("/usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf", font_size)
            except:
                font = ImageFont.load_default()
            ch = random.choice(chs)
            y_pos = int(y + i * font_size * speed)
            color = (0, min(255, 120 + op), 0, min(255, 60 + op))
            draw.text((x, y_pos % (h+200) - 100), ch, font=font, fill=color)
    
    # Add title box with glitch lines
    try:
        title_font = ImageFont.truetype("/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf", 36)
        sub_font = ImageFont.truetype("/usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf", 16)
    except:
        title_font = ImageFont.load_default()
        sub_font = ImageFont.load_default()

    # Add semi-transparent panel
    panel_h = 90
    panel = Image.new("RGBA", (w-80, panel_h), (0,0,0,150))
    panel_draw = ImageDraw.Draw(panel)
    # thin neon border
    panel_draw.rectangle([0,0,w-80-1,panel_h-1], outline=(0,200,0,180))
    img.paste(panel, (40, h - panel_h - 30), panel)

    # Draw title and subtitle on panel
    tx = 60
    ty = h - panel_h - 10
    draw.text((tx, ty+10), title, font=title_font, fill=accent)
    draw.text((tx, ty+52), subtitle, font=sub_font, fill=(160,220,160,255))

    # Add small repo badge area
    badge = Image.new("RGBA", (160,34), (0,0,0,200))
    bd = ImageDraw.Draw(badge)
    bd.rectangle([0,0,159,33], outline=(0,150,0,180))
    try:
        bfont = ImageFont.truetype("/usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf", 14)
    except:
        bfont = ImageFont.load_default()
    bd.text((8,6), "github.com/Mishbahop", font=bfont, fill=(120,255,120,255))
    img.paste(badge, (w-180, h-54), badge)

    # Save PNG (optimize)
    img.save(filename, optimize=True, quality=90)

# Create three thumbnails
thumbs = [
    ("/mnt/data/thumbnails/project_ai_voice.png", "AI Voice Chatbot", "Speech -> Intent -> Action"),
    ("/mnt/data/thumbnails/cyber_portfolio.png", "Cyber Portfolio", "Matrix-styled Personal Site"),
    ("/mnt/data/thumbnails/game_engine.png", "Lightweight Game Engine", "2D physics + WebGL renderer")
]

for path, t, s in thumbs:
    draw_matrix_thumb(path, t, s)

# List files for user and provide paths
files = os.listdir("/mnt/data/thumbnails")
files_paths = [f"/mnt/data/thumbnails/{f}" for f in files]
files_paths

