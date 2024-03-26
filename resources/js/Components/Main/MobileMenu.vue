<script setup>
import { Link } from '@inertiajs/vue3';
import { Badge } from '@/Components/ui/badge';
import { Button } from '@/Components/ui/button';
import { Sheet, SheetContent, SheetTrigger } from '@/Components/ui/sheet';
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/Components/ui/card';
import { Home, LineChart, Menu, Package, PlaneTakeoff, ShoppingCart, Users } from 'lucide-vue-next';
</script>
<template>
    <Sheet>
        <SheetTrigger as-child>
            <Button variant="outline" size="icon" class="shrink-0 md:hidden">
                <Menu class="h-5 w-5" />
                <span class="sr-only">Toggle navigation menu</span>
            </Button>
        </SheetTrigger>
        <SheetContent side="left" class="flex flex-col">
            <nav class="grid gap-2 text-lg font-medium">
                <Link href="/dashboard" class="flex items-center gap-2 text-lg font-semibold mb-8">
                <PlaneTakeoff class="h-6 w-6" />
                <span>Larajet</span>
                </Link>
                <Link href="/dashboard"
                    class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground"
                    :class="route().current('dashboard') ? 'bg-muted text-primary' : 'text-muted-foreground'">
                <Home class="h-5 w-5" />
                Dashboard
                </Link>
                <a href="#"
                    class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground">
                    <ShoppingCart class="h-5 w-5" />
                    Orders
                    <Badge class="ml-auto flex h-6 w-6 shrink-0 items-center justify-center rounded-full">
                        6
                    </Badge>
                </a>
                <a href="#"
                    class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground">
                    <Package class="h-5 w-5" />
                    Products
                </a>
                <a href="#"
                    class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground">
                    <Users class="h-5 w-5" />
                    Customers
                </a>
                <a href="#"
                    class="mx-[-0.65rem] flex items-center gap-4 rounded-xl px-3 py-2 text-muted-foreground hover:text-foreground">
                    <LineChart class="h-5 w-5" />
                    Analytics
                </a>
            </nav>
            <div class="mt-auto">
                <Card>
                    <CardHeader>
                        <CardTitle>Upgrade to Pro</CardTitle>
                        <CardDescription>
                            Unlock all features and get unlimited access to our
                            support team.
                        </CardDescription>
                    </CardHeader>
                    <CardContent>
                        <Button size="sm" class="w-full">
                            Upgrade
                        </Button>
                    </CardContent>
                </Card>
            </div>
        </SheetContent>
    </Sheet>
</template>