/* See LICENSE file for copyright and license details. */
#include <X11/XF86keysym.h>

/* appearance */
static const unsigned int borderpx  = 2;        /* border pixel of windows */
static const unsigned int gappx     = 6;        /* gaps between windows */
static const unsigned int snap      = 32;       /* snap pixel */
static const unsigned int systraypinning = 0;   /* 0: sloppy systray follows selected monitor, >0: pin systray to monitor X */
static const unsigned int systrayonleft = 1;           /* 0: systray in the right corner, >0: systray on left of status text */
static const unsigned int systrayspacing = 2;   /* systray spacing */
static const int systraypinningfailfirst = 1;   /* 1: if pinning fails, display systray on thee first monitor, False: display systray on the last monitor*/
static const int showsystray        = 1;     /* 0 means no systray */
static const int showbar            = 1;        /* 0 means no bar */
static const int topbar             = 1;        /* 0 means bottom bar */
static const char *fonts[]          = { "monospace:size=12" };
static const char dmenufont[]       = "monospace:size=12";
static const char blue[]            = "#26232a";
static const char black[]	    = "#000000";
static const char purple[]	    = "#5b4b8c";
static const char *colors[][3]      = {
	/*               fg         bg         border   */
	[SchemeNorm] = { purple, blue, blue },
	[SchemeSel]  = { black, purple, purple    },
};

/* tagging */
static const char *tags[] = { "1", "2", "3", "4", "5", "6", "7", "8", "9" };

static const Rule rules[] = {
	/* xprop(1):
	 *	WM_CLASS(STRING) = instance, class
	 *	WM_NAME(STRING) = title
	 */
	/* class                          instance    title       tags mask     isfloating   monitor */
	{ "Gimp",                         NULL,       NULL,       0,            1,           -1 },
	{ "Firefox", 	                  NULL,       "Firefox Preferences",       1 << 8,       0,           -1 },
	{ "nm-connection-editor",         NULL,       NULL,       ~0,           1,           -1 },
	{ "Steam",			  NULL,       "Friends List",		0,	         1,	      -1 },
};

/* layout(s) */
static const float mfact     = 0.55; /* factor of master area size [0.05..0.95] */
static const int nmaster     = 1;    /* number of clients in master area */
static const int resizehints = 1;    /* 1 means respect size hints in tiled resizals */
static const int lockfullscreen = 1; /* 1 will force focus on the fullscreen window */

static const Layout layouts[] = {
	/* symbol     arrange function */
	{ "[]=",      tile },    /* first entry is default */
	{ "><>",      NULL },    /* no layout function means floating behavior */
	{ "[M]",      monocle },
};

/* key definitions */
#define MODKEY Mod4Mask
#define TAGKEYS(KEY,TAG) \
	{ MODKEY,                       KEY,      view,           {.ui = 1 << TAG} }, \
	{ MODKEY|ControlMask,           KEY,      toggleview,     {.ui = 1 << TAG} }, \
	{ MODKEY|ShiftMask,             KEY,      tag,            {.ui = 1 << TAG} }, \
	{ MODKEY|ControlMask|ShiftMask, KEY,      toggletag,      {.ui = 1 << TAG} },

/* helper for spawning shell commands in the pre dwm-5.0 fashion */
#define SHCMD(cmd) { .v = (const char*[]){ "/bin/sh", "-c", cmd, NULL } }

/* commands */
static char dmenumon[2] = "0"; /* component of dmenucmd, manipulated in spawn() */
static const char *dmenucmd[] = { "dmenu_run", "-m", dmenumon, "-fn", dmenufont, "-nb", blue, "-nf", purple, "-sb", purple, "-sf", black, NULL };
static const char *termcmd[]  = { "alacritty", NULL };
static const char *librewolf[] = { "librewolf", NULL };
static const char *icecat[] = { "icecat", NULL};
static const char *firefox[] = { "firefox", NULL };
static const char *steamcmd[] = { "steam", NULL };
static const char *filemancmd[] = { "pcmanfm", NULL };
static const char *tutanota[] = { "tutanota-desktop", NULL };
static const char *strawberry[] = { "strawberry", NULL };
//volume controls

//This is for no pulseaudio support

//static const char *upvol[]   = { "amixer", "-q", "set", "Master", "5%+", "unmute", NULL };
//static const char *downvol[] = { "amixer", "-q", "set", "Master", "5%-", "unmute", NULL };
//static const char *mutevol[] = { "amixer", "-q", "set", "Master", "toggle", NULL };

//This is for pulseaudio support

static const char *upvol[]   = { "amixer", "-q", "-D", "pulse", "set", "Master", "5%+", "unmute", NULL };
static const char *downvol[] = { "amixer", "-q", "-D", "pulse", "set", "Master", "5%-", "unmute", NULL };
static const char *mutevol[] = { "amixer", "-q", "-D", "pulse", "set", "Master", "toggle", NULL };

//This is for pulseaudio on Laptops

//static const char *upvol[]   = { "pulsemixer", "--change-volume", "+10", "--unmute", NULL };
//static const char *downvol[] = { "pulsemixer", "--change-volume", "-10", "--unmute", NULL };
//static const char *mutevol[] = { "pulsemixer", "--toggle-mute", NULL };

//keyboard controls
static const char *kbrightup[] = { "asusctl", "-n", NULL };
static const char *kbrightdown[] = { "asusctl", "-p", NULL };
static const char *aura[] = { "asusctl", "led-mode", "-n", NULL };
static const char *fan[] = { "asusctl", "profile", "-n", NULL };
static const char *touchpad[] = { "exec /usr/bin/toggle-touchpad.sh", "NULL" };

static Key keys[] = {
	/* modifier                     key        function        argument */
	{ MODKEY,                       XK_r,      spawn,          {.v = dmenucmd } },
	{ MODKEY,                       XK_Return, spawn,          {.v = termcmd } },
	{ MODKEY,			XK_b,	   spawn,          {.v = librewolf } },
	{ MODKEY|ControlMask,           XK_b,      spawn,          {.v = firefox } },
	{ MODKEY|ControlMask|ShiftMask, XK_b,      spawn,          {.v = icecat } },
	{ MODKEY,			XK_t,	   spawn,	   {.v = steamcmd } },
	{ MODKEY,			XK_e,	   spawn,	   {.v = filemancmd } },
	{ MODKEY,                       XK_p,      spawn,          {.v = tutanota } },
	{ MODKEY,                       XK_f,      spawn,          {.v = strawberry } },
	{ MODKEY|ShiftMask,             XK_b,      togglebar,      {0} },
	{ MODKEY,                       XK_j,      focusstack,     {.i = +1 } },
	{ MODKEY,                       XK_k,      focusstack,     {.i = -1 } },
	{ MODKEY,                       XK_i,      incnmaster,     {.i = +1 } },
	{ MODKEY,                       XK_d,      incnmaster,     {.i = -1 } },
	{ MODKEY,                       XK_h,      setmfact,       {.f = -0.05} },
	{ MODKEY,                       XK_l,      setmfact,       {.f = +0.05} },
	{ MODKEY,                    XK_backslash, zoom,           {0} },
	{ MODKEY,                       XK_Tab,    view,           {0} },
	{ MODKEY,                    XK_BackSpace, killclient,     {0} },
	{ MODKEY|ShiftMask,             XK_t,      setlayout,      {.v = &layouts[0]} },
	{ MODKEY|ShiftMask,             XK_f,      setlayout,      {.v = &layouts[1]} },
	{ MODKEY|ShiftMask,             XK_m,      setlayout,      {.v = &layouts[2]} },
	{ MODKEY|ShiftMask,             XK_space,  setlayout,      {0} },
	{ MODKEY|ShiftMask,         XK_backslash,  togglefloating, {0} },
	{ MODKEY,                       XK_0,      view,           {.ui = ~0 } },
	{ MODKEY|ShiftMask,             XK_0,      tag,            {.ui = ~0 } },
	{ MODKEY,                       XK_comma,  focusmon,       {.i = -1 } },
	{ MODKEY,                       XK_period, focusmon,       {.i = +1 } },
	{ MODKEY|ShiftMask,             XK_comma,  tagmon,         {.i = -1 } },
	{ MODKEY|ShiftMask,             XK_period, tagmon,         {.i = +1 } },
	TAGKEYS(                        XK_1,                      0)
	TAGKEYS(                        XK_2,                      1)
	TAGKEYS(                        XK_3,                      2)
	TAGKEYS(                        XK_4,                      3)
	TAGKEYS(                        XK_5,                      4)
	TAGKEYS(                        XK_6,                      5)
	TAGKEYS(                        XK_7,                      6)
	TAGKEYS(                        XK_8,                      7)
	TAGKEYS(                        XK_9,                      8)
	{ MODKEY|ShiftMask,             XK_q,      quit,           {0} },
	{ 0,	     XF86XK_AudioRaiseVolume,	   spawn,          {.v = upvol } },
	{ 0,	     XF86XK_AudioLowerVolume,      spawn,	   {.v = downvol } },
	{ 0,                XF86XK_AudioMute,      spawn,	   {.v = mutevol } },
	{ 0,	      XF86XK_KbdBrightnessUp,	   spawn,	   {.v = kbrightup } },
	{ 0,	    XF86XK_KbdBrightnessDown,	   spawn,	   {.v = kbrightdown } },
	{ 0,                  XF86XK_Launch3,	   spawn,	   {.v = aura } },
	{ 0,		      XF86XK_Launch4,	   spawn,	   {.v = fan } },
	{ 0,	       XF86XK_TouchpadToggle,	   spawn,	   {.v = touchpad } },
        
};

/* button definitions */
/* click can be ClkTagBar, ClkLtSymbol, ClkStatusText, ClkWinTitle, ClkClientWin, or ClkRootWin */
static Button buttons[] = {
	/* click                event mask      button          function        argument */
	{ ClkLtSymbol,          0,              Button1,        setlayout,      {0} },
	{ ClkLtSymbol,          0,              Button3,        setlayout,      {.v = &layouts[2]} },
	{ ClkWinTitle,          0,              Button2,        zoom,           {0} },
	{ ClkStatusText,        0,              Button2,        spawn,          {.v = termcmd } },
	{ ClkClientWin,         MODKEY,         Button1,        movemouse,      {0} },
	{ ClkClientWin,         MODKEY,         Button2,        togglefloating, {0} },
	{ ClkClientWin,         MODKEY,         Button3,        resizemouse,    {0} },
	{ ClkTagBar,            0,              Button1,        view,           {0} },
	{ ClkTagBar,            0,              Button3,        toggleview,     {0} },
	{ ClkTagBar,            MODKEY,         Button1,        tag,            {0} },
	{ ClkTagBar,            MODKEY,         Button3,        toggletag,      {0} },
};

