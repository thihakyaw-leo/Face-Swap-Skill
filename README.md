# Face-Swap-Skill

ဒီ repository က Manus ရဲ့ video-generation skill နဲ့ အထောက်အကူပြု workflow reference များကို စုစည်းထားပါတယ်။ `SKILL.md` သည် agent အတွက် လမ်းညွှန်ဖြစ်ပြီး `references/` အတွင်းရှိ ဖိုင်များသည် သီးခြားအခြေအနေများအတွက် အသေးစိတ် guide များဖြစ်သည်။ ဒီဖိုင်တွေက VisoMaster ကို install လုပ်ပေးတဲ့ software သို့မဟုတ် တိုက်ရိုက် run လုပ်နိုင်တဲ့ script မဟုတ်ပါ။

## Repository ထဲက ဖိုင်များ

- [`SKILL.md`](SKILL.md) — ရှိပြီးသား footage ကို transform လုပ်ခြင်း၊ identity/outfit references ပြင်ဆင်ခြင်း၊ အပိုင်းတို စမ်းသပ်ခြင်းနှင့် output စစ်ဆေးခြင်းဆိုင်ရာ အဓိက skill။
- [`references/higgsfield-genjutsu.md`](references/higgsfield-genjutsu.md) — Genjutsu ကို conceptual reference အဖြစ်သုံးပြီး motion transfer နှင့် object/wardrobe swap ကို ခွဲခြားစဉ်းစားရန်။ အခြား tools တွင် အဲဒီ capability ရှိမည်ဟု အာမခံခြင်းမဟုတ်ပါ။
- [`references/visomaster-pipeline.md`](references/visomaster-pipeline.md) — VisoMaster Fusion ကဲ့သို့ compatible local editor ရှိသည့်အခါ face-swap, multi-face tracking, mask/composite နှင့် face restoration လုပ်ငန်းစဉ်အတွက် လမ်းညွှန်။

## VisoMaster local pipeline guide ကို အသုံးပြုပုံ

### ဘယ်အခါမှာ အသုံးပြုသင့်သလဲ

`references/visomaster-pipeline.md` ကို **ကိုယ့်စက်မှာ VisoMaster Fusion (သို့) လက်ရှိအသုံးပြုနေသော compatible editor ရှိပြီး** အောက်ပါအလုပ်များကို လုပ်မည်ဆိုလျှင် ဖတ်ပါ။

- video ထဲက မျက်နှာတစ်ခု သို့မဟုတ် အများအပြားကို သတ်မှတ်ထားသော identity ဖြင့် face-swap လုပ်ခြင်း၊
- လူများဖြတ်ကျော်ခြင်း၊ ပျောက်ကွယ်ပြီးပြန်ပေါ်လာခြင်း၊ scene cut ဖြစ်ခြင်းတို့အတွင်း face track များကို စစ်ဆေးခြင်း၊
- mask/compositing အမှားများကို ပြင်ခြင်း၊
- လိုအပ်သည့်အခါ face-level restoration သို့မဟုတ် full-frame enhancement လုပ်ခြင်း။

ဒီ guide သည် **လုပ်ထုံးလုပ်နည်း reference** သာဖြစ်သည်။ Manus ရဲ့ video-generation tool က VisoMaster သို့မဟုတ် ၎င်း၏ local model များကို အလိုအလျောက် run နိုင်သည်ဟု မဆိုလိုပါ။ App, model weights, UI/CLI နဲ့ hardware ကို သီးခြားစစ်ဆေးပါ။ VisoMaster version နှင့် interface ကွာနိုင်သောကြောင့် အရင်ဆုံး လက်ရှိ official manual ကိုကြည့်ပါ။

### လုပ်ငန်းစဉ် အကျဉ်း

1. **မူရင်းကို ထိန်းသိမ်းပါ။** Original footage ကို copy/backup လုပ်ပြီး output ကို ဖိုင်အသစ်အဖြစ် သိမ်းပါ။ အရင်ဆုံး အခက်ခဲဆုံး pose, lighting, occlusion ပါသော စက္ကန့်အနည်းငယ်ကို စမ်းပါ။
2. **ခွင့်ပြုထားသော identity များသာ သုံးပါ။** Source face card တစ်ခုစီကို မှန်ကန်သော identity နှင့်ချိတ်ပါ။ လူအစစ်၏ likeness ကို သုံးရန် သဘောတူညီချက်နှင့် အသုံးပြုခွင့်ကို စစ်ပါ။ Face crop/embedding များကို biometric data အဖြစ် သဘောထားပြီး local storage ကို ဦးစားပေးပါ။
3. **Track mapping ကို render မတိုင်မီ အတည်ပြုပါ။** Scene အစ၊ ဖြတ်ကူးချိန်၊ occlusion နောက်၊ scene cut နောက်နှင့် frame ထဲမှ ထွက်/ပြန်ဝင်ချိန်တို့မှာ target face တစ်ခုစီကို မှန်ကန်သော card နှင့် တွဲထားကြောင်း preview လုပ်ပါ။
4. **Model နှင့် face controls ကို အဆင့်လိုက်ညှိပါ။** Swapper များကို တူညီသော test frame/settings ဖြင့် A/B စမ်းပါ။ Neutral swap မှစပြီး geometry, expression, mask ကို ပြဿနာမြင်ရသည့်နေရာတွင်သာ အနည်းငယ်ချင်းပြင်ပါ။ Restoration က မျက်နှာအသေးစိတ်ကို ပြောင်းလဲနိုင်သဖြင့် raw swap နှင့် နှိုင်းယှဉ်ပါ။
5. **Full render မတိုင်မီ review လုပ်ပါ။** Frame များနှင့် normal-speed playback ကို စစ်ပြီး identity, edges, occlusion, flicker, audio sync နှင့် output dimensions ကို အတည်ပြုပါ။ စမ်းသပ်မှုအောင်မြင်မှသာ full clip ကို render လုပ်ပါ။

အဆင့်တစ်ခုချင်းစီ၏ အသေးစိတ်နှင့် ဆုံးဖြတ်ချက်များကို [`VisoMaster pipeline guide`](references/visomaster-pipeline.md) တွင်ကြည့်ပါ။ Model code နှင့် model weights တို့၏ license မတူနိုင်သဖြင့် download/redistribute/commercial use မလုပ်မီ သီးခြားစီ စစ်ပါ။

### Full-body အဝတ်အစားပြောင်းလဲခြင်းနှင့် မတူပါ

VisoMaster guide သည် အဓိကအားဖြင့် **မျက်နှာ/ခေါင်းပိုင်း** ကို ပြုပြင်ရန်ဖြစ်ပြီး လူ၏ ကိုယ်ခန္ဓာပုံစံ၊ pose၊ တစ်ကိုယ်လုံးအဝတ်အစား သို့မဟုတ် scene တစ်ခုလုံးကို ယုံကြည်စိတ်ချစွာ ပြောင်းရန် မဟုတ်ပါ။ Full-body wardrobe transformation လိုအပ်ပါက source video motion ကို ထိန်းသိမ်းနိုင်သည့် video-to-video/whole-character tool ကို စစ်ဆေးပြီး [`Higgsfield Genjutsu reference`](references/higgsfield-genjutsu.md) ကို workflow ခွဲခြားစဉ်းစားရန်သာ အသုံးပြုပါ။ လက်ရှိ tool တွင် အဲဒီစွမ်းရည် မရှိပါက အဲဒီအချက်ကို ရှင်းပြပြီး face-only swap ကို အစားထိုးအဖြစ် တိတ်တဆိတ် မသုံးပါနှင့်။

## Remote VS Code Server-ээр алсын GPU машинд ашиглах

VS Code Server/Remote Tunnels нь алсын машин дээрх VS Code editor болон terminal-д холбогдох боломж өгдөг. Энэ нь VisoMaster суулгахгүй, GPU/VRAM нэмэхгүй, мөн graphical desktop-ийг remote-desktop маягаар дамжуулахгүй. Тушаал болон видео боловсруулалт алсын host дээр ажиллах тул тухайн host өөрөө VisoMaster-ийн дэмждэг OS, ажиллах GPU/driver, RAM болон disk space-тай байх ёстой. Microsoft-ийн баримтаар нэг VS Code Server instance нь нэг user/client-д зориулагдсан; бусдад зориулсан hosted service болгон санал болгохыг license зөвшөөрдөггүй ([VS Code Server docs](https://code.visualstudio.com/docs/remote/vscode-server), [license terms](https://aka.ms/vscode-server-license)).

1. **Алсын host-оо бэлд.** VisoMaster Fusion болон шаардлагатай model weights-ийг тухайн OS-д зориулсан албан ёсны зааврын дагуу суулга. Апп GPU-г үнэхээр таньж байгааг шалга. Model weights-ийн тусгай license-ийг мөн унш.
2. **GUI шаардлагыг шалга.** VS Code Server нь code/editor/terminal access болохоос VisoMaster-ийн цонхыг харуулах баталгаа биш. Хэрэв суулгасан VisoMaster workflow graphical UI шаардвал тусдаа, зөвшөөрөгдсөн remote-desktop арга хэрэглэх эсвэл VisoMaster-ийн албан ёсоор баримтжуулсан CLI/headless горимыг ашигла. Тийм горим байна гэж таамаглан тушаал зохиож болохгүй.
3. **Хувийн tunnel нээ.** Алсын host дээр Microsoft-ийн [Remote Tunnels зааврыг](https://code.visualstudio.com/docs/remote/tunnels) дагаж `code tunnel` CLI-г ажиллуулах эсвэл VS Code UI-аас **Turn on Remote Tunnel Access**-ийг сонго. License-ийн нөхцөлийг уншаад зөвшөөр; анхны тохиргоог license-ийн мэдэгдлийг алгасуулан автоматжуулахгүй.
4. **Өөрийн VS Code client-оос холбо.** Tunnel үүсгэсэнтэй ижил нэвтрэх account-аар баталгаажуулаад Command Palette-аас **Remote Tunnels: Connect to Tunnel**-ийг сонгон remote workspace-ийг нээ. Тэндээс файл, terminal болон GPU status-ийг шалгана; туннель өөрөө GPU-г дамжуулахгүй.
5. **Богино тестээс эхэл.** Remote host дээр эх видеоны copy ашиглаж хэдхэн секундын хүнд хэсгийг туршаад [`VisoMaster pipeline guide`](references/visomaster-pipeline.md)-ийн track, mask, output review дарааллыг дага. Source, face cards/embeddings болон output-ийг зөвшөөрөлтэй remote disk дээр хамгаалж хадгал.
6. **Ажлаа дуусгахад tunnel-ээ зогсоо.** CLI tunnel-ийг ажиллуулсан terminal дээр `Ctrl+C` дар, эсвэл VS Code UI-аас tunnel-ийг унтраа. Нэг instance-д олон хүн зэрэг холбохгүй, бусдад үйлчилгээ болгон share/host хийхгүй; tunnel-ийг зөвхөн өөрийн эрхтэй development session-д ашигла.

Face footage, face cards болон embeddings нь эмзэг мэдээлэл тул remote workspace-ийн access ба хадгалах хугацааг хязгаарла. Хүсвэл Microsoft-ийн баримтад дурдсан `code tunnel --disable-telemetry` сонголтоор VS Code Server telemetry-г унтрааж болно; энэ нь VisoMaster болон бусад extension-ийн telemetry тохиргоог өөрчлөхгүй ([telemetry guidance](https://code.visualstudio.com/docs/remote/vscode-server#_telemetry)).

## Repo ကို ယူသုံးရန်

```bash
git clone https://github.com/thihakyaw-leo/Face-Swap-Skill.git
cd Face-Swap-Skill
```

ရှိပြီးသား clone ကို update လုပ်ရန် `git pull origin main` ကို run လုပ်ပါ။ ထို့နောက် လုပ်မည့်အလုပ်နှင့်ကိုက်ညီသော reference ကိုဖတ်ပါ။
